---
description: |
  Automatically detect, fetch, and summarize URLs found in triggering GitHub issue.
  Posts summary as comments on issue to provide context without leaving GitHub.

on:
  issues:
    types: [opened, edited]
  workflow_dispatch:

strict: false

permissions:
  contents: read
  issues: read

network:
  allowed:
    - "*"

engine: 
  id: claude
  model: claude-haiku-4-5

tools:
  github:
    lockdown: false
    toolsets: [repos, issues]
  bash: [":*"] 
  web-fetch:  

safe-outputs:
  add-comment:
    max: 3                       # max comments (default: 1)
    target: "*"                  # "triggering" (default), "*", or number

---

# Automated Link Summarization for Triggering GitHub Issue

1. Extract all URLs from the triggering issue body (markdown links, plain URLs, code-fenced URLs)
2. Skip internal GitHub links (issues, PRs, commits in the same repository)
3. Fetch and summarize the content (2-3 sentences highlighting main topic, key points, and relevance)
4. Post a single comment with all summaries, formatted with original URL, page title, and summary
5. If issue is edited, update the existing bot comment rather than creating a new one

### Error Handling
- Gracefully handle inaccessible URLs (404s, timeouts, blocked content)
- Note when a link cannot be fetched with brief explanation
- Continue processing remaining links if one fails
- Default maximum: 10 links per issue