# README: Getting Started with Workflows in Next.js

Welcome to the Getting Started guide for the Workflow DevKit in a Next.js environment. This document provides a step-by-step guide to setting up and running your first workflow.

## Core Concepts

This guide will walk you through the essential configuration steps and introduce you to the core concepts of workflows and steps. By the end of this guide, you will have a solid understanding of how to get up and running with the Workflow DevKit in a Next.js environment.

---

## Setup and Configuration

The Next.js getting started guide provides a hands-on tutorial for setting up your first workflow. The key steps are:

1.  **Create a new Next.js project**: If you don't have one already.
2.  **Install the `workflow` package**: `npm i workflow`
3.  **Configure Next.js**: Wrap your `next.config.ts` with `withWorkflow()`. This is a crucial step that enables the necessary code transformations for the `"use workflow"` and `"use step"` directives.

---

## Your First Workflow

The guide will then walk you through creating your first workflow, which will include:

-   A **workflow function** (`"use workflow"`) that orchestrates the steps.
-   Several **step functions** (`"use step"`) that perform the actual work.
-   A **route handler** that triggers the workflow.

By following this guide, you will gain a practical understanding of how to build, configure, and run workflows in a Next.js application.


