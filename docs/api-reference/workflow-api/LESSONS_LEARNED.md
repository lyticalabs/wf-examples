# Lessons Learned: API Reference - Workflow API

This document summarizes the key takeaways from the `api-reference/workflow-api` documentation.

- **`index.mdx`**: The `workflow/api` package provides the essential functions for interacting with workflows from outside the workflow itself. This includes starting new workflows (`start`), resuming paused workflows (`resumeHook`, `resumeWebhook`), and checking the status of a running workflow (`getRun`). These functions are the bridge between your application and the workflow engine, allowing you to control the lifecycle of your workflows.

- **`get-run.mdx`**: `getRun()` is a vital function for monitoring the status of a workflow without having to wait for it to complete. By providing a `runId`, you can get immediate access to the workflow's metadata, including its current status, timing information, and any output streams. This is essential for building user interfaces that show the progress of a workflow, or for creating monitoring systems that track the health of your workflows.

- **`resume-hook.mdx`**: `resumeHook()` is the counterpart to `createHook()`, and it's used to send a payload to a paused workflow. This is the mechanism by which external systems can provide data to a workflow and cause it to resume execution. By calling `resumeHook()` with the hook's token and a payload, you can unblock a workflow and allow it to continue with the new data.

- **`resume-webhook.mdx`**: `resumeWebhook()` is the counterpart to `createWebhook()`, and it's used to forward an HTTP `Request` to a paused workflow. This is the mechanism by which external systems can communicate with a workflow via HTTP. By calling `resumeWebhook()` with the webhook's token and a `Request` object, you can unblock a workflow and allow it to continue, optionally returning a custom `Response` to the caller.

- **`start.mdx`**: The `start()` function is the primary way to initiate a new workflow execution from your application code. It enqueues the workflow and its arguments for processing, and immediately returns a `Run` object with the `runId`. This is an asynchronous operation, so you can use the `runId` with `getRun()` to monitor the workflow's progress without blocking your application.
