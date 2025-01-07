# Blogs Repository

This repository contains Markdown files designed to be rendered using **Hugo** instead of GitHub's default Jekyll rendering.

## Purpose of the Repository

The primary purpose of this repository is to **test and refine a GitHub Actions CI/CD workflow** that automates the rendering of Markdown files into HTML using Hugo. This workflow is under development and will eventually be used for our other repository, **[Notefy](https://github.com/your-username/notefy)**, where Markdown files are currently rendered by Jekyll.

### Why Hugo?

We have decided to move from Jekyll to Hugo for the following reasons:
- **Speed**: Hugo generates static sites faster than Jekyll.
- **Flexibility**: Hugo's support for custom themes and configurations aligns better with our long-term goals.

This repository serves as a **sandbox environment** to ensure that the Hugo-based workflow is fully functional before migrating Notefy.

## Workflow Development

The GitHub Actions workflow for automating Hugo rendering is still a **work in progress**. Once completed, it will:
1. Detect changes in Markdown files.
2. Trigger Hugo to render the Markdown into HTML.
3. Deploy the rendered content to the appropriate hosting platform or branch.

For more details about GitHub Actions workflows, visit the documentation: [GitHub Actions Overview](https://solidpoint.ai/s/Z_7RIuf_Z-Q).

### Planned Usage for Notefy

Once the workflow is finalized and tested here, it will be applied to **Notefy**, our repository for Markdown notes. This will complete the migration of Notefy from Jekyll to Hugo, enabling a more streamlined rendering process.

## How to Contribute

Feel free to explore and contribute to this repository by:
1. Testing the rendering process with new Markdown files.
2. Providing feedback or suggestions for the GitHub Actions workflow.

To contribute, fork this repository, make your changes, and open a pull request.

---

Stay tuned for updates as we continue building and refining the workflow!
