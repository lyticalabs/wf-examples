# Lessons Learned: API Reference - Workflow AI

This document summarizes the key takeaways from the `api-reference/workflow-ai` documentation.

- **`index.mdx`**: The `@workflow/ai` package provides specialized tools for building AI-powered workflows. It includes the `DurableAgent` class for creating stateful AI agents that can execute tools with automatic retries, and the `WorkflowChatTransport` for ensuring reliable communication with AI models, even in the presence of interruptions. These tools are essential for building robust and resilient AI applications on top of the workflow engine.

- **`durable-agent.mdx`**: The `DurableAgent` class is a powerful abstraction for creating stateful, resilient, and interactive AI agents. It seamlessly integrates with the workflow engine, allowing you to define tools that are executed as durable steps with automatic retries. This makes it easy to build complex AI-powered workflows that can interact with external systems, wait for human input, and recover from failures without losing state.

- **`workflow-chat-transport.mdx`**: `WorkflowChatTransport` is a specialized chat transport for the AI SDK that provides reliable, resumable message streaming. It's designed to work with workflow-based chat applications, automatically reconnecting to interrupted streams and ensuring that no messages are lost. This is crucial for building robust chat applications that can handle network issues, page refreshes, and other interruptions without disrupting the user experience.
