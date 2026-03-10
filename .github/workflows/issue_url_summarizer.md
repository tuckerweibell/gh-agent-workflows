---
description: |
  Output the env for debugging using bash tool.

on:
  issues:
    types: [opened, edited]
  workflow_dispatch:

strict: false

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

# Output env with bash tool
Output env so I can debug.
