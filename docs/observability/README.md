# README: Workflow Observability

Welcome to the guide on workflow observability. This document provides an in-depth overview of the tools that the Workflow DevKit provides for inspecting, monitoring, and debugging your workflows.

## Core Concepts

The Workflow DevKit provides a powerful set of observability tools, including a CLI and a web UI, that allow you to gain deep insights into the execution of your workflows. These tools are essential for debugging issues, monitoring the health of your workflows, and understanding how your workflows are behaving in different environments.

---

## Observability Tools

-   **CLI**: The `workflow` CLI provides a command-line interface for inspecting workflow runs, steps, and events. It's a great tool for quick checks and for integrating with your existing command-line workflows.
-   **Web UI**: The Workflow DevKit also includes a local web UI that provides a more visual and interactive way to explore your workflows. You can launch the web UI with the `--web` flag in the CLI.

---

## Connecting to Different Environments

The observability tools can connect to any "World," which means you can use them to monitor workflows in both local development and production environments. This is a powerful feature that allows you to use the same tools and workflows for debugging and monitoring, regardless of where your workflows are running.

-   **Local Development**: By default, the observability tools connect to your local development environment.
-   **Production**: To connect to a production environment, you can use the `--backend` flag to specify the "World" you want to connect to. For example, to connect to Vercel, you would use `--backend vercel`.


