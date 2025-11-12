# Lessons Learned: API Reference - Workflow Next

This document summarizes the key takeaways from the `api-reference/workflow-next` documentation.

- **`index.mdx`**: The `workflow/next` package is the key to integrating the workflow engine with a Next.js application. It provides the `withWorkflow` function, which automatically configures the necessary webpack/turbopack loaders to transform your workflow code. This seamless integration makes it easy to get started with workflows in a Next.js environment.

- **`with-workflow.mdx`**: The `withWorkflow` function is the main entry point for integrating the workflow engine with your Next.js application. By wrapping your `nextConfig` with this function, you enable the necessary code transformations that allow you to use the `"use step"` and `"use workflow"` directives. This is a simple but crucial step that makes it possible to write and execute workflows within a Next.js project.
