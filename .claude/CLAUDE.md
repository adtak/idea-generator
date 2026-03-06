# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

This is a **Claude Code skill** repository. It defines a single skill (`idea-generator`) that generates product and service proposals from a seed text file.

There is no build system, runtime, or test runner. The primary artifacts are:

- `idea-generator/SKILL.md` — orchestrator (flow control only, ~30 lines)
- `idea-generator/agents/seed-generator.md` — seed auto-generation logic
- `idea-generator/agents/proposal-generator.md` — idea filtering and proposal generation rules
- `idea-generator/references/proposal-template.md` — Markdown template for each proposal
- `idea-generator/references/output-constraints.md` — non-negotiable output rules
- `idea-generator/evals/evals.json` — eval cases for validating skill output quality
- `idea-generator/evals/files/` — seed text files used as eval inputs

## Skill Behavior

The `idea-generator` skill:

1. Checks whether a seed file was provided
2. If no seed file: reads `agents/seed-generator.md` and generates a seed inline
3. Reads `agents/proposal-generator.md` and generates 3–5 proposals filtered by: solo-shippable scope (~3 months MVP), clear differentiation, believable monetization path, no exotic dependencies
4. Outputs each proposal using the template in `references/proposal-template.md`
5. Ends with a ranked recommendation

Tech stack and implementation details are **intentionally out of scope**. Covers any type of product or service — mobile apps, web services, SaaS tools, physical products, and more.

## Evals

Evals are defined in `idea-generator/evals/evals.json`. Each eval has:
- `prompt` — the user message (may be in Japanese)
- `expected_output` — description of what a passing response looks like
- `files` — seed files the skill must read
- `expectations` — checklist of required output properties

The seed files and eval prompts may be in Japanese. Proposals should match the language the user writes in (Japanese prompt → Japanese output).

## Modifying the Skill

When editing files, preserve:
- The proposal template structure in `references/proposal-template.md` exactly — evals check for specific sections (Target Audience table, Monetization table, Go-to-Market Phases table, Scorecard with star ratings)
- The ranked recommendation at the end of multi-proposal output
- The constraint in `references/output-constraints.md` that prohibits tech stack / architecture sections
- The `agents/` files are plain Markdown read by SKILL.md via the Read tool — they are not registered Claude Code sub-agents and do not need YAML frontmatter
