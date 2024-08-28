---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---

# Archyve

Archyve is a Document Library for indexing documents and searching them for relevant chunks of text. These chunks can be used in a RAG flow to provide additional context to LLMs.

## Why?

### 1. Document Awareness

LLMs work well enough when prompted about subjects from their training data, but cannot answer questions about private documents.

Archyve enables LLMs to answer questions about your private documents as if they were part of its training data, while letting you keep your documents safely and privately on your infrastructure.

### 2. Document-centric approach

Its document-centric approach allows you to maintain a large set of pre-embedded and graphed documents, so relevant data can be pulled into any LLM prompt without the need to choose relevant documents yourself and upload them to a chat.

### 3. Knowledge Graph

Archyve has a Knowledge Graph (KG) feature that allows it to provide insights into your documents that go beyond a baseline retrieval-augmented generation approach, improving quality and accuracy. It's based on Microsoft's [Graph RAG project](https://github.com/microsoft/graphrag).

## API

Archyve's API can be access under `/v1`. Resources include:

- `/v1/search?q=<query>`
  - search a collection
  - returns a list of document chunks with URL and distance
- `/v1/chat?prompt=<prompt>&model=<model>&augment=<true|false>&collections=<collection_ids>`
  - send a chat prompt and return the response
- `/v1/collections`
  - list collections (of documents)
- `/v1/collections/:id`
  - get data on one collection
- `/v1/collections/:id/search?q=<query>`
  - search a collection
  - returns a list of document chunks with URL and distance
- `/v1/chunks/:id`
  - retrieve a chunk, including its content
- `/v1/collections/:id/entities/:id`
  - retrieve an entity, including its content and metadata
- `/v1/collections/:id/documents`
  - list documents in a collection
- `/v1/collections/:id/documents/:id`
  - retrieve a document's metadata
- `/v1/collections/:id/documents/:id/chunks`
  - list chunks in a document
- `/v1/collections/:id/documents/:id/chunks/:id`
  - retrieve a chunk's content and metadata
- `/v1/version`
  - get version information about the running instance of Archyve

OpenAPI spec coming soon.

### Authentication

Archyve uses a client ID and Bearer token for authenticating API clients.

If you are in the `development` environment, i.e. `$environment` is not set, Archyve will create default client credentials the first time it starts. It will then print the credentials to the console:

```
To authenticate with the default API client, set these headers:

Authorization: Bearer ...
X-Client-Id: ...

E.g.:

curl -v localhost:3300/v1/collections \
  -H "Accept: application/json" \
  -H "Authorization: Bearer ..." \
  -H "X-Client-Id: ..."
```

Include these headers it specifies in any request to the API.

## UI

The UI has two main areas for users:

1. Documents
2. Chat

Documents allows a user to upload and index documents, view which documents are in the system, reindex existing documents, and set Facts.

Chat presents a basic chat interface where the user can test the effectiveness of their indexing. The user can select which document collections are searched by the system and have relevant chunks from those document collections added to their prompt before the prompt is sent to an LLM. The response is streamed to the user.

Typical usage of Archyve's UI is anticipated to be:

- configure ingest settings and select models
- ingest documents
- use chat to test ingest settings and models

Once the user is satisfied with the document indexing, they can have another application, such as [HuggingFace Chat UI](https://github.com/huggingface/chat-ui) or [Open WebUI](https://github.com/open-webui/open-webui), use Archyve's API to search for relevant chunks of text and add them to a prompt before sending it to an LLM.
