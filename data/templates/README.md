# Project Templates

Reusable building blocks for `::proj` project creation. Templates are composed based on project type — not copied wholesale.

## How It Works

1. User types `::proj [description]`
2. Agent runs a 3-4 question interview (all multiple choice except optional final question)
3. Agent selects the right project type
4. Project type determines which template blocks are included
5. Agent generates the project document

## Project Types → Template Blocks

| Block              | Feature Build | Testing | Research | Refactor | Other |
|--------------------|:---:|:---:|:---:|:---:|:---:|
| Header             |  x  |  x  |  x  |  x  |  x  |
| Executive Summary  |  x  |  x  |  x  |  x  |     |
| Version History    |  x  |  x  |     |  x  |     |
| Tasks              |  x  |  x  |  x  |  x  |  x  |
| Success Criteria   |  x  |  x  |  x  |     |     |
| Results Matrix     |     |  x  |     |     |     |
| Test Protocol      |     |  x  |     |     |     |
| Findings           |     |  x  |  x  |  x  |     |
| Notes              |  x  |  x  |  x  |  x  |  x  |
| Session Log        |  x  |  x  |  x  |  x  |  x  |
