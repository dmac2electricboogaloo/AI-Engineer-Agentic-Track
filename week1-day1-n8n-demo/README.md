# Week 1, Day 1: An Agentic Workflow

Day 1 has two lectures:

1. **Part 1:** a no-code demo of what an AI agent is, built in n8n. The rest of the course builds agents in code; this is a preview of the idea.
2. **Part 2:** an overview of the six-week course, how it fits with the instructor's other courses, and who it suits. Notes are at the end of this file.

## Part 1: n8n demo

### What an agent is

An AI agent is an LLM called in a loop with tools to achieve a goal. This demo shows it in three stages:

1. **LLM only:** behaves like a normal chat model.
2. **LLM plus one tool:** it looks up a live stock price.
3. **LLM plus three tools:** it reads and writes a Google Sheet by itself, deciding which tool to use and when.

### What I built

A chat-triggered n8n workflow with an AI Agent node connected to:

- **Model:** OpenAI chat model (GPT-5.4 Mini)
- **Memory:** Simple Memory
- **Tools:**
  - Marketstack: latest stock price, with the ticker chosen by the model
  - Google Sheets, get rows: reads the portfolio sheet
  - Google Sheets, append row: adds a trade, with ticker and share count chosen by the model

![Full workflow](images/01-full-workflow.png)

### Setup

- n8n account (free 14-day trial)
- OpenAI API key
- Marketstack API key (free tier)
- A Google Sheet called `Investments` with two rows: Amazon (10 shares) and Apple (2 shares)

### Steps

1. Create a workflow and add a chat trigger.
   ![Chat trigger](images/02-chat-trigger.png)
2. Add an AI Agent node, then attach the OpenAI model and Simple Memory.
   ![Agent node](images/03-agent-node.png)
3. Test the plain LLM with a greeting and a fun fact.
   ![Plain LLM test](images/04-plain-llm.png)
4. Add the Marketstack tool (ticker chosen by the model, return all, "latest" filter on), then ask for the price of Apple.
   ![Marketstack tool](images/05-marketstack-tool.png)
5. Add the two Google Sheets tools with these descriptions:
   - Get rows: *Get rows in the Google Sheets to retrieve my stock portfolio details.*
   - Append row: *append a row in order to add a new trade with a new quantity of your choosing.*
   ![Sheets tools](images/06-sheets-tools.png)
6. Run the autonomy demo with these prompts in order:
   1. "What's the value of my stock portfolio?"
   2. "Please come up with a suggestion for an investment to balance my portfolio. Add your suggestion to my sheet. You decide the ticker and the number of shares."
   3. "Yes, please add something defensive to balance of your choosing."
   ![Autonomy demo](images/07-autonomy-demo.png)

### Results

*(Fill in after running it: what the agent valued the portfolio at, which tickers and share counts it chose, and anything that surprised me.)*

![Final sheet](images/08-final-sheet.png)

### What I took from it

- The agent picks tools based on the descriptions written for them, so descriptions matter.
- Nothing is actually bought. The agent only writes rows to the sheet.
- Results differ run to run, since the model chooses its own tickers and quantities.

### Files

- [`workflow.json`](./workflow.json): exported n8n workflow (checked for secrets before committing)

## Part 2: Course overview and roadmap

### What the course covers

The course has three strands: the theory of agents (design patterns, architectures, MCP), the agent frameworks themselves (using and comparing them), and applying them to commercial projects. The instructor frames the difference from his other coding courses this way: this one is about *building* agents with code, while his AI Coder course is about *using* prebuilt agents (Claude Code, Codex, Cursor and similar) to write software.

### Six-week roadmap

| Week | Focus | Projects named in the lecture |
|------|-------|-------------------------------|
| 1 | Foundations: the theory that the rest of the course builds on | Personal digital twin (a career chatbot, deployed) |
| 2 | OpenAI Agents SDK (the instructor's favorite framework) | Automated sales development rep; deep research app |
| 3 | CrewAI | Stock picker; a simulated engineering team (front end, back end, lead, tester) |
| 4 | LangGraph, popular in enterprise | Sidekick |
| 5 | Rapid tour of other frameworks: Google ADK with A2A, AWS Strands Agents, other Python frameworks and some JavaScript/TypeScript ones | Agent Loop |
| 6 | Model Context Protocol (MCP) | Equity Traders in Action (the grand finale) |

Each week has five days. In the lecture's roadmap graphic, boxes are color-coded: orange for theory days, blue for days that introduce a new framework, and yellow for the eight project deliverables. The folders in the instructor's code repo follow the same order (`1_foundations` through `6_mcp`).

Notes:
- The project count of eight is the instructor's. My list above has eight names, which matches if the digital twin and the stock picker both count as projects. That is my reading, so check it against the course page.
- Week 5 is new in this version. It replaces a week on Autogen, which Microsoft has put on hold.
- MCP appears throughout the course, not only in week 6.

### How to take the course

- **Order:** Take the weeks in order. Each builds on the last. Someone in a hurry could do weeks 1 and 2 and then jump to week 6, but week 6 assumes fluency with the OpenAI Agents SDK from week 2.
- **Week 1 is worth doing.** The instructor expects people to be tempted to skip it, and says it gives the clarity that the rest depends on.
- **Who it suits:** People who know some Python and have worked a little with LLMs. Complete beginners can take it but face a steep curve. A set of self-study guides in the `guides` folder of the course repo covers that gap.
- **Experienced agent builders** are encouraged to push the projects further and contribute them back to the course repo.
- **Instructor support:** Ed Donner answers questions through Udemy Q&A and email.

### How his other courses relate

| Course | What it covers |
|--------|----------------|
| AI Builder | No-code agents with n8n and ElevenLabs (a stepping stone to this course) |
| AI Coder | Using coding agents (Claude Code, Codex, Antigravity, Copilot, Cursor) to write code |
| AI Leader | The business side of delivering AI projects |
| AI Engineer Core Track | LLM foundations, plus RAG and fine-tuning |
| AI Engineer Agentic Track | This course |
| AI Engineer Production Track | Making LLM and agent projects scalable, resilient and observable (his most advanced) |

The three AI Engineer tracks overlap very little and can be taken in any order. Someone new to LLMs would get the most from the first two weeks of the Core Track before this one.

### About the instructor

Ed Donner is co-founder and CTO of nebula.io. He spent most of his career in Wall Street technology at J.P. Morgan, rising to managing director over about 300 engineers and data scientists, and earlier founded an AI startup, Untappd, which was acquired.

### Transcript notes

The lecture transcripts were generated by speech-to-text and contain errors. Names I corrected from context: "Cloud Code" is Claude Code, "Landgraf" is LangGraph, "crew AI" is CrewAI, and "aistartupnebula.io" is nebula.io. The transcript also says the Sidekick project is in week 6 at one point, but he places it in week 4 when he lists the weeks in order, so I treated week 6 as a slip.
