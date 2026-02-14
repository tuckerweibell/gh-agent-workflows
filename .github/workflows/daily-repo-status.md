---
description: |
  Automatically detect, fetch, and summarize URLs found in GitHub issue bodies.
  Posts summaries as comments to provide context without leaving GitHub.

on:
  issues:
    types: [opened, edited]
  workflow_dispatch:

permissions:
  contents: read
  issues: read
  pull-requests: read

strict: false

network:
  allowed:
    - "*"

engine: claude

tools:
  github:
  bash: [":*"] 
  web-fetch:  
---

# Automated Link Summarization for GitHub Issues

1. Extract all URLs from the issue body (markdown links, plain URLs, code-fenced URLs)
2. Skip internal GitHub links (issues, PRs, commits in the same repository)
3. For each external URL, check if authentication is needed
4. Fetch and summarize the content (2-3 sentences highlighting main topic, key points, and relevance)
5. Post a single comment with all summaries, formatted with original URL, page title, and summary
6. If issue is edited, update the existing bot comment rather than creating a new one

### Error Handling
- Gracefully handle inaccessible URLs (404s, timeouts, blocked content)
- Note when a link cannot be fetched with brief explanation
- Continue processing remaining links if one fails
- Default maximum: 10 links per issue