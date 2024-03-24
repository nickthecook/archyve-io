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

- `/documents`
  - list documents
- `/search?q=<query>`
  - search documents
  - returns a list of documents with URL and distance (score)
- `/facts`
  - list facts (not yet implemented)

OpenAPI spec coming soon.

### Authentication

Archyve uses a Bearer token for authentication. Your request should include the header:

```
Authorization: Bearer <token>
```

All API results are scoped to the user to which the API key belongs.

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

Once the user is satisfied with the document indexing, they can have another application, such as HuggingFace Chat UI, use Archyve's API to search for relevant chunks of text and add them to a prompt before sending it to an LLM.
