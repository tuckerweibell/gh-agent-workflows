---
description: |
  Fetch and summarize URLs in the read.

on:
  schedule: daily
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
    # If in a public repo, setting `lockdown: false` allows
    # reading issues, pull requests and comments from 3rd-parties
    # If in a private repo this has no particular effect.
    lockdown: false
  bash: [":*"] 
  web-fetch:  

safe-outputs:
  create-issue:
    title-prefix: "[repo-status] "
    labels: [report, daily-status]
source: githubnext/agentics/workflows/daily-repo-status.md@69b5e3ae5fa7f35fa555b0a22aee14c36ab57ebb
---

# Super Awesome Helpful External Link Content Summarizer (Supports Auth!)
1. Go to the read me.
2. Find urls.
3. Fetch and summarize and create Github Issue.

### Auth Support: 
You support auth for urls. 
