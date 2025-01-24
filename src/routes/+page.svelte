<script>
	import { writable } from 'svelte/store';
	import { marked } from 'marked';

	const renderedHTML = writable('');
	const errorMessage = writable('');
	let isLoading = false;
	let url = 'http://localhost:8000/api/v1/chat/completions';
	let headers = JSON.stringify(
		{
			'Content-Type': 'application/json',
			Accept: 'text/event-stream'
		},
		null,
		2
	);
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
		try {
			isLoading = true;
			errorMessage.set('');
			renderedHTML.set('');

			const customHeaders = JSON.parse(headers);
			const response = await fetch(url, {
				method: 'POST',
				headers: customHeaders,
				body
			});

			if (!response.ok) {
				throw new Error(`HTTP error! status: ${response.status}`);
			}

			const reader = response.body?.getReader();
			if (!reader) {
				throw new Error('Server response was empty');
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
		} catch (error) {
			console.error('Error:', error);
			// @ts-ignore
			if (error.name === 'TypeError' && error.message.includes('fetch')) {
				errorMessage.set(
					'Unable to reach the server. Please check if the URL is correct and the server is running.'
				);
			} else {
				// @ts-ignore
				errorMessage.set(`Error: ${error.message}`);
			}
		} finally {
			isLoading = false;
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
		<label for="headers">Request Headers (JSON):</label>
		<textarea id="headers" bind:value={headers} rows="5"></textarea>
	</div>

	<div>
		<label for="body">Request Body (JSON):</label>
		<textarea id="body" bind:value={body} rows="10"></textarea>
	</div>

	{#if $errorMessage}
		<div class="error-message">
			{$errorMessage}
		</div>
	{/if}

	<button type="submit" disabled={isLoading} class:loading={isLoading}>
		{#if isLoading}
			<span class="loader"></span>
		{/if}
		{isLoading ? 'Sending...' : 'Send Request'}
	</button>
</form>

<article class="card prose">
	{@html $renderedHTML}
</article>

<style>
	.error-message {
		background-color: #fee2e2;
		border: 1px solid #ef4444;
		color: #dc2626;
		padding: 0.75rem;
		border-radius: 0.375rem;
		margin: 1rem 0;
	}

	button {
		position: relative;
	}

	button:disabled {
		opacity: 0.7;
		cursor: not-allowed;
	}

	.loading {
		padding-left: 2.5rem;
	}

	.loader {
		position: absolute;
		left: 1rem;
		width: 1rem;
		height: 1rem;
		border: 2px solid #ffffff;
		border-bottom-color: transparent;
		border-radius: 50%;
		display: inline-block;
		animation: rotation 1s linear infinite;
	}

	@keyframes rotation {
		0% {
			transform: rotate(0deg);
		}
		100% {
			transform: rotate(360deg);
		}
	}
</style>
