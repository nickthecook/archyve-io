---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
---

# Archyve

Archyve is a Document Library for indexing documents and searching them for relevant chunks of text. These chunks can be used in a RAG flow to provide additional context to LLMs.

## Why?

Different documents have different, and sometimes strange, indexing requirements. While chat UIs sometimes include RAG features like accepting document uploads and indexing them, there are many documents that need special processing before they can be indexed. This is where Archyve comes in.

Archyve takes this concern away from chat UIs and other LLM-based applications, so they can focus on what they do best.

## API

Archyve's API can be access under `/v1`. Resources include:

- `/search?q=<query>`
  - search a collection
  - returns a list of document chunks with URL and distance
- `/collections`
  - list collections (of documents)
- `/collections/:id`
  - get data on one collection
- `/collections/:id/search?q=<query>`
  - search a collection
  - returns a list of document chunks with URL and distance
- `/chunks/:id`
  - retrieve a chunk, including its content

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

> To force Archyve to recreate the default client, delete your development database and restart Archyve.

## UI

The UI has two main areas:

1. Documents
2. Chat

Documents allows a user to upload and index documents, view which documents are in the system, reindex existing documents, and set Facts.

Chat presents a basic chat interface where the user can test the effectiveness of their indexing. The user can select which document collections are searched by the system and have relevant chunks from those document collections added to their prompt before the prompt is sent to an LLM. The response is streamed to the user.

Typical usage of Archyve's UI is anticipated to be:

- index documents
- use chat to test indexing parameters
- tweak indexing parameters
- use chat to test indexing parameters
- etc.

Once the user is satisfied with the document indexing, they can have another application, such as [HuggingFace Chat UI](https://github.com/huggingface/chat-ui) or [Open WebUI](https://github.com/open-webui/open-webui), use Archyve's API to search for relevant chunks of text and add them to a prompt before sending it to an LLM.
