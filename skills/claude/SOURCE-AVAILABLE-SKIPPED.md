# Source-available skills — not vendored here

The following skills in anthropics/skills are source-available (not
open-source). Anthropic permits personal use and reference but not
redistribution. We do not vendor them into this repo:

- docx/ — Word document creation/editing
- pdf/ — PDF creation/editing
- pptx/ — PowerPoint creation/editing
- xlsx/ — Excel creation/editing

To use them locally, clone them directly from upstream:

    git clone --depth 1 https://github.com/anthropics/skills /tmp/claude-skills
    cp -r /tmp/claude-skills/skills/{docx,pdf,pptx,xlsx} ~/my-local-skills/

Upstream: https://github.com/anthropics/skills — see the "About This
Repository" section of their README for exact terms.
