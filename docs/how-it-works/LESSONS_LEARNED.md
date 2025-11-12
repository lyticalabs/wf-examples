# Lessons Learned: How It Works

This document summarizes the key takeaways from the `how-it-works` documentation.

- **`code-transform.mdx`**: The `"use workflow"` and `"use step"` directives are the key to the Workflow DevKit's durable execution model. They trigger a code transformation process that separates the workflow's orchestration logic from its side effects. This allows the workflow to be replayed deterministically, while the steps are executed with full access to the Node.js runtime. Understanding this transformation is key to understanding how the workflow engine works.

- **`framework-integrations.mdx`**: Integrating the Workflow DevKit with a framework involves two main components: a build-time step to generate the workflow handler files, and a runtime step to expose these handlers as HTTP endpoints. The documentation provides a clear example of how to do this with Bun, and the same principles can be applied to any JavaScript runtime.

- **`understanding-directives.mdx`**: The `"use workflow"` and `"use step"` directives are a critical part of the Workflow DevKit's design. They provide a clear, compile-time signal that a function has special execution semantics. This allows the compiler to perform the necessary transformations to enable durable execution, and it provides a clear signal to the developer that they are writing code that will be executed in a special context. The documentation provides a detailed explanation of why directives were chosen over other approaches, such as decorators or file-based conventions.
