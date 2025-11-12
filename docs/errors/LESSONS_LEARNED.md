# Lessons Learned: Errors

This document summarizes the key takeaways from the `errors` documentation.

- **`index.mdx`**: The `errors` documentation provides a valuable resource for troubleshooting common issues when working with the Workflow DevKit. It covers a range of topics, from proper usage of `fetch` and Node.js modules to handling serialization failures and webhook response issues. This centralized guide is a great starting point for resolving common errors and understanding the best practices for building reliable workflows.

- **`fetch-in-workflow.mdx`**: Workflow functions run in a sandboxed environment and do not have direct access to the global `fetch()` function. To make HTTP requests from within a workflow, you must use the `fetch` step function provided by the `workflow` package. For libraries like the AI SDK that use `fetch()` internally, you can make it available by assigning `globalThis.fetch = fetch` at the beginning of your workflow.

- **`node-js-module-in-workflow.mdx`**: Due to the sandboxed nature of workflow functions, you cannot directly use Node.js core modules like `fs`, `http`, or `crypto`. Any code that relies on these modules must be moved into a separate step function, which has full access to the Node.js runtime. This separation is crucial for maintaining the determinism and replayability of your workflows.

- **`serialization-failed.mdx`**: Serialization is a fundamental concept in the workflow engine, and it's essential to understand that all data passed between workflows and steps must be serializable. This means you can't pass functions, class instances, or other non-serializable types as arguments or return values. Instead, you should pass plain data and reconstruct any necessary objects or logic within the step or workflow.

- **`start-invalid-workflow-function.mdx`**: The `start()` function requires a valid workflow function that has been correctly processed by the build system. This error occurs when the provided function is missing the `"use workflow"` directive, the Next.js configuration is not wrapped with `withWorkflow()`, or the wrong function is being imported. It's a reminder to double-check these common configuration issues when setting up your workflows.

- **`webhook-invalid-respond-with-value.mdx`**: When creating a webhook, the `respondWith` option can only be set to `"manual"`, a `Response` object, or be left `undefined` for a default `202 Accepted` response. This error occurs when you provide an invalid value, such as a plain object or an incorrect string. It's a reminder to use the correct values to ensure your webhooks respond as expected.

- **`webhook-response-not-sent.mdx`**: When you create a webhook with `respondWith: "manual"`, you are responsible for sending a response using `request.respondWith()`. This error occurs when the workflow finishes without sending a response, leaving the original HTTP request hanging. It's crucial to ensure that all code paths, including error conditions, send a response when using manual response mode.
