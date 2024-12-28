<script>
	import { writable } from 'svelte/store';
	import { marked } from 'marked';

	const renderedHTML = writable('');
	let url = 'http://localhost:8000/api/v1/chat/completions';
	let body = JSON.stringify(
		{
			job_id: '3fa85f64-5717-4562-b3fc-2c963f66afa6',
			message: 'Hey there, how to make a todo list app in sveltekit?',
			role: 'user',
			message_type: 'text'
		},
		null,
		2
	);

	async function handleSubmit() {
		const response = await fetch(url, {
			method: 'POST',
			headers: {
				'Content-Type': 'application/json',
				Accept: 'text/event-stream'
			},
			body
		});

		const reader = response.body?.getReader();
		if (!reader) {
			console.error('No reader found');
			return;
		}
		const decoder = new TextDecoder();

		let accumulatedText = '';

		while (true) {
			const { value, done } = await reader.read();
			if (done) break;

			const chunk = decoder.decode(value, { stream: true });
			const lines = chunk.split('\n');

			for (const line of lines) {
				if (line.startsWith('data: ')) {
					let text = line.slice(6);
					text = text.replaceAll('[NEWLINE]', '\n');

					if (text === '[DONE]') {
						return;
					}

					accumulatedText += text;
					const html = await marked(accumulatedText);
					renderedHTML.set(html);
				}
			}
		}
	}
</script>

<form on:submit|preventDefault={handleSubmit} class="card">
	<div>
		<label for="url">Endpoint URL:</label>
		<div class="input-group">
			<span class="method-tag">POST</span>
			<input type="text" id="url" bind:value={url} placeholder="Enter your SSE endpoint URL" />
		</div>
	</div>

	<div>
		<label for="body">Request Body (JSON):</label>
		<textarea id="body" bind:value={body} rows="10"></textarea>
	</div>

	<button type="submit">Send Request</button>
</form>

<article class="card prose">
	{@html $renderedHTML}
</article>
