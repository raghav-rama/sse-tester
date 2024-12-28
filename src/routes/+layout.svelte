<script>
	import '../app.css';
</script>

<div class="container">
	<header>
		<h1>SSE Tester</h1>
		<p>
			Test your Server-Sent Events endpoints with this interactive tool. Enter your endpoint URL and
			request body below to start streaming responses.
		</p>
	</header>

	<main>
		<slot />
	</main>

	<footer>
		<div class="card">
			<h2>About SSE Tester</h2>
			<p>
				SSE Tester is a free, open-source tool designed to help developers test and debug
				Server-Sent Events (SSE) endpoints. Perfect for testing streaming APIs like ChatGPT-style
				implementations, real-time notifications, and live data feeds.
			</p>

			<h3>Key Features:</h3>
			<ul>
				<li>Test any SSE endpoint with custom URLs and request bodies</li>
				<li>Real-time response streaming with markdown support</li>
				<li>JSON request body editor</li>
				<li>Clean, simple UI</li>
			</ul>

			<h3>Common Use Cases:</h3>
			<ul>
				<li>Testing AI streaming responses</li>
				<li>Debugging SSE implementations</li>
				<li>Validating real-time data streams</li>
				<li>Monitoring event sources</li>
			</ul>
		</div>
	</footer>
</div>

<style>
	footer {
		margin-top: 3rem;
	}

	h2 {
		font-size: 1.5rem;
		color: #60a5fa;
		margin-bottom: 1rem;
	}

	h3 {
		font-size: 1.2rem;
		color: #e5e7eb;
		margin: 1.5rem 0 0.5rem 0;
	}

	ul {
		list-style-type: disc;
		margin-left: 1.5rem;
		color: #d1d5db;
	}

	li {
		margin: 0.5rem 0;
	}
</style>
