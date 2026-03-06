---
name: idea-generator
description: |
  Generates product and service ideas from a seed file or domain hint, and outputs structured project proposals in Markdown.
  Covers any type of product or service — mobile apps, web services, SaaS tools, physical products, and more.
  Produces proposals covering target audience, core features, monetization strategy, go-to-market phases, and competitive landscape.
  Tech stack and implementation details are intentionally out of scope.

  TRIGGER: Use this skill whenever the user wants to brainstorm product or service ideas, generate a
  project proposal, or turn a seed file into a concrete concept — even if they phrase it casually like
  "I want to build something" or "give me product ideas" or "help me figure out what to make."
argument-hint: "[product-or-service]"
disable-model-invocation: true
allowed-tools: Read, Write
---

# Product & Service Idea Generator

## Process

1. Check whether the user has provided a seed file path as an argument.

2. **If no seed file was provided:** Read `agents/seed-generator.md` and follow it to generate a seed inline. Show the result to the user, then continue.
   **If a seed file was provided:** Read the specified file.

3. Read `agents/candidate-generator.md` and follow it:
   - Extract key signals from the seed
   - Generate 8–10 candidate ideas in a structured table

4. Read `agents/idea-selector.md` and follow it:
   - Score all candidates on 4 axes and select exactly 3

5. Read `agents/proposal-writer.md` and follow it:
   - Write full proposals for the 3 selected ideas, using `references/proposal-template.md`

6. Ask the user (or infer from context) whether to save to a file or print inline. If saving, use Write.
