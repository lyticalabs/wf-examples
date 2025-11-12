# Lessons Learned: Deploying

This document summarizes the key takeaways from the `deploying` documentation.

- **`index.mdx`**: The concept of "Worlds" is central to deploying workflows. Worlds are adapters that connect your workflow code to the underlying infrastructure, handling storage, queuing, and authentication. This abstraction allows the same workflow code to run seamlessly in different environments, from local development to production. The documentation highlights the built-in worlds for local development and Vercel, and provides a path for creating custom worlds for other platforms.


