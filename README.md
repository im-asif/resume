# asif-public1

## Content quality checks

The repository includes a CI workflow for content validation:

- Markdown structure linting (`markdownlint-cli`)
- Strict site build validation (`hugo --panicOnWarning`)
- Link validation (`lychee`)

To run the strict build locally:

```bash
hugo --panicOnWarning
```
