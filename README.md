# AI Engineer Agentic Track: The Complete Agent & MCP Course

My working notes, workflows and code from the Udemy course *AI Engineer Agentic Track: The Complete Agent & MCP Course*. The course runs six weeks and covers eight projects, moving from a no-code agent demo to building agents in code and connecting them to tools through MCP (Model Context Protocol).

This repo holds my own work: notes written in my own words, screenshots from my runs, exported workflows, and code I write or modify. It does not include any course videos or slides.

## Course code

The instructor's code for the course, taught by Ed Donner, is in his public repo, [ed-donner/agents](https://github.com/ed-donner/agents) (MIT license). I run it from my own local clone and keep my notes and experiments here. Credit for the course material and original code goes to him.

## Progress

| Week | Day | Topic | Folder |
|------|-----|-------|--------|
| 1 | 1 | Build a first autonomous agent with n8n (no-code demo) | [week1-day1-n8n-demo](./week1-day1-n8n-demo) |

I'll add a row for each day as I complete it.

## How the repo is organized

- One folder per day, named `weekN-dayN-topic`.
- Each folder has its own `README.md` with notes, steps and screenshots (`images/`).
- Workflows are exported as JSON and code lives alongside the notes.

## A note on secrets

API keys and credentials are never committed. Code reads keys from a local `.env` file, which is listed in `.gitignore`. Exported n8n workflows are checked for keys, tokens and email addresses before being pushed.

## About

Built by David McIntyre as part of a hands-on move into agentic AI engineering, building on 13+ years of SAP Ariba and Source-to-Pay experience.
