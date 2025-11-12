# README: Deploying Workflows

Welcome to the guide on deploying workflows. This document provides an in-depth overview of the "World" concept, which is central to running workflows in different environments.

## The "World" Concept

A **World** is an adapter that connects your workflow code to the underlying infrastructure. It's a powerful abstraction that handles storage, queuing, and authentication, allowing the same workflow code to run seamlessly in different environments, from local development to production.

The `World` interface provides a consistent way for workflows to interact with the outside world, regardless of the specific platform they are running on. This makes it possible to write portable, reusable workflow logic that can be deployed anywhere.

---

## Built-in Worlds

The Workflow DevKit comes with two built-in worlds:

-   **Vercel World**: The recommended `World` for production deployments on Vercel. It's a fully managed, scalable, and secure backend that's seamlessly integrated with the Vercel platform. It provides automatic configuration, multi-environment support, and robust queuing and storage, making it the easiest way to run workflows in production.

---

## Custom Worlds

In addition to the built-in worlds, you can also create your own custom `World`s to run workflows on other platforms. The documentation provides a reference implementation for a **Postgres World**, which demonstrates how to build a custom `World` backed by a PostgreSQL database.

The Postgres World uses `pg-boss` for job queuing and PostgreSQL's `NOTIFY`/`LISTEN` for real-time streaming. While not recommended for production use, it serves as a valuable example of how to create a durable, multi-host `World` for running workflows in a non-serverless environment.


