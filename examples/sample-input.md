# Sample Input

## Conversation A — 2026-08-10

**Learner:** What is an API, and why does an AI product need one?

**Assistant:** An API is a defined interface that allows software systems to exchange requests and responses. In an AI product, the frontend commonly calls a backend API, and the backend securely calls a model provider.

## Conversation B — 2026-08-11

**Learner:** Does the frontend call the model directly? Where should the API key go?

**Assistant:** Production frontends should not expose model API keys. The frontend calls a backend endpoint; the backend reads the key from a protected secret store and calls the model provider.

## Conversation C — 2026-08-11

**Learner:** I still do not understand how the frontend talks to the backend.

**Assistant:** The frontend sends an HTTP request to a backend API endpoint. The backend validates the request, runs business logic, and returns a structured response.
