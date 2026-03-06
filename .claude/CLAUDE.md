# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repo Is

This is a **Claude Code skill** repository. It defines a single skill (`idea-generator`) that Claude Code can invoke to generate iOS app project proposals from a seed text file.

There is no build system, runtime, or test runner. The primary artifacts are:

- `idea-generator/SKILL.md` — the skill definition (prompt + behavior spec)
- `idea-generator/evals/evals.json` — eval cases for validating skill output quality
- `idea-generator/evals/files/` — seed text files used as eval inputs

## Skill Behavior

The `idea-generator` skill:

1. Reads a user-specified seed file (interests, pain points, domain notes)
2. Generates 3–5 iOS app proposals filtered by: solo-shippable scope (~3 months MVP), clear monetization path, buildable with Expo + AWS
3. Outputs each proposal using the structured Markdown template defined in `SKILL.md`
4. Ends with a ranked recommendation

**Fixed tech stack** (do not suggest alternatives unless the user asks):
- Frontend: Expo (React Native) + TypeScript, Expo Router, Zustand or TanStack Query
- Backend: AWS Lambda + API Gateway, DynamoDB, S3, Cognito

## Evals

Evals are defined in `idea-generator/evals/evals.json`. Each eval has:
- `prompt` — the user message (may be in Japanese)
- `expected_output` — description of what a passing response looks like
- `files` — seed files the skill must read
- `assertions` — checklist of required output properties

The seed files and eval prompts may be in Japanese. Proposals should match the language the user writes in (Japanese prompt → Japanese output).

## Modifying the Skill

When editing `SKILL.md`, preserve:
- The proposal template structure exactly — evals assert on specific sections (Target Audience table, Monetization table, AWS architecture table, Development Phases table, Scorecard with star ratings)
- The ranked recommendation at the end of multi-proposal output
- The fixed tech stack assumption
