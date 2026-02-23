Agentic AI Workflow for Technical Support Email Automation

This project implements an Agentic AI workflow designed to automate responses to technical support emails using a documentation-driven Retrieval-Augmented Generation (RAG) system.

The goal is to eliminate repetitive manual responses to common technical queries. Instead of a human repeatedly referring to documentation and drafting responses, this workflow intelligently detects relevant emails, retrieves accurate context from documentation, generates a response, and replies automatically — significantly improving efficiency.

The entire system runs locally using the n8n self-hosted AI starter kit to avoid API rate limits and maintain full control over the pipeline.

Workflow Design

The system operates through two independent trigger points: one for documentation updates and one for incoming emails.

1. Client-Side Trigger – Documentation Update

When a new document is uploaded to Google Drive:

The workflow detects the upload.

The document is chunked.

Embeddings are generated.

The content is indexed into Qdrant (vector database).

This allows the knowledge base to update dynamically without redeploying the system. Documentation changes are reflected immediately, ensuring the workflow remains responsive and up-to-date.

2. User-Side Trigger – Incoming Email

When a new email is received:

A classification step determines whether the email is related to technical support.

If it is not, the workflow takes no action.

If it is:

The email is passed to an AI agent.

The agent queries Qdrant using the email content.

Relevant documentation chunks are retrieved.

A response is generated.

The system sends an automated reply on behalf of the user.

Technical Stack

Workflow Engine: n8n (self-hosted)

Vector Database: Qdrant

Models Used:

Qwen2.5-7B – used for chunking, retrieval, and text classification

Llama3.2-latest – used for response generation

Starter Kit Repository:
https://github.com/n8n-io/self-hosted-ai-starter-kit

Model Selection Rationale

Smaller models were initially tested for embedding, retrieval, and classification. However, their performance was inconsistent and often inaccurate for semantic matching and classification tasks.

Qwen2.5-7B provided significantly better contextual understanding and stability, making it suitable for retrieval and classification in this workflow.

For response generation, Llama3.2 was chosen due to its strong instruction-following capability and consistent, well-structured output suitable for professional email communication.

Summary

This project demonstrates a practical implementation of an agentic RAG system for real-world business automation. By combining intelligent classification, vector retrieval, and automated response generation, the workflow removes repetitive manual effort while maintaining documentation-grounded accuracy.
