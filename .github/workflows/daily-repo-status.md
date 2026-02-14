---
description: |
  This workflow creates daily repo status reports based on the README.md

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

# Daily Repo Status

Create a status reports based on the README.md or info in the README.md. You may need to fetch this.

## What to include

- README or content fetched from README

## Style

- Be positive, encouraging, and helpful

## Process

1. Check out the README
2. Gather data as needed
3. Create a new GitHub issue with your findings
