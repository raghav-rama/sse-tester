# SSE Tester

A simple web-based tool to test Server-Sent Events (SSE) endpoints.

https://github.com/user-attachments/assets/08c646b4-ec0c-4da2-9030-61420818c897

## Features

- Test any SSE endpoint with custom JSON payloads
- Real-time markdown rendering of streamed responses
- Error handling for network issues and invalid responses
- Visual loading states and feedback
- Support for streaming markdown content

## Setup

1. Clone the repository
2. Install dependencies:

```bash
pnpm install
```

3. Start the development server:

```bash
pnpm dev
```

## Usage

1. Enter your SSE endpoint URL in the input field
2. Modify the JSON request body as needed
3. Click "Send Request" to start the stream
4. The response will be rendered in real-time with markdown support

## Default Configuration

The app comes pre-configured with:

- Default endpoint: `http://localhost:8000/api/v1/chat/completions`
- Request method: `POST`
- Headers:
  - `Content-Type: application/json`
  - `Accept: text/event-stream`

## Error Handling

The app handles various error scenarios:

- Network connectivity issues
- Invalid server responses
- Empty responses
- HTTP error status codes
