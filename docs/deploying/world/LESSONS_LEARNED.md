# Lessons Learned: Deploying - World

This document summarizes the key takeaways from the `deploying/world` documentation.

- **`index.mdx`**: The `World` interface is a powerful concept that allows you to abstract the underlying infrastructure from your workflow logic. By providing a consistent interface for storage, queuing, and authentication, `World`s make it possible to run the same workflow code in different environments without modification. The documentation highlights the built-in `World`s for local development and V-ercel, as well as community-provided `World`s for other platforms like Postgres and Jazz.

- **`postgres-world.mdx`**: The Postgres World is a reference implementation that demonstrates how to build a custom `World` backed by a PostgreSQL database. It uses `pg-boss` for job queuing and PostgreSQL's `NOTIFY`/`LISTEN` for real-time streaming. While not recommended for production use, it serves as a valuable example of how to create a durable, multi-host `World` for running workflows in a non-serverless environment.

- **`vercel-world.mdx`**: The Vercel World is the recommended `World` for production deployments on Vercel. It's a fully managed, scalable, and secure backend that's seamlessly integrated with the Vercel platform. It provides automatic configuration, multi-environment support, and robust queuing and storage, making it the easiest way to run workflows in production.
