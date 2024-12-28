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
				<li class="source-code">
					Source code available on GitHub
					<a
						href="https://github.com/raghav-rama/sse-tester"
						target="_blank"
						rel="noopener noreferrer"
						aria-label="GitHub Repository"
					>
						<svg height="24" width="24" viewBox="0 0 16 16" class="github-icon">
							<path
								fill="currentColor"
								d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z"
							></path>
						</svg>
					</a>
				</li>
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

	.source-code {
		display: flex;
		align-items: center;
		gap: 0.5rem;
	}

	.github-icon {
		color: #d1d5db;
		transition: color 0.2s ease;
	}

	.github-icon:hover {
		color: #60a5fa;
	}
</style>
