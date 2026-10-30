# Week 1, Day 1: First Autonomous Agent with n8n

A no-code demo of what an AI agent is, built in n8n. The rest of the course builds agents in code; this day is a preview of the idea.

## What an agent is

An AI agent is an LLM called in a loop with tools to achieve a goal. This demo shows it in three stages:

1. **LLM only:** behaves like a normal chat model.
2. **LLM plus one tool:** it looks up a live stock price.
3. **LLM plus three tools:** it reads and writes a Google Sheet by itself, deciding which tool to use and when.

## What I built

A chat-triggered n8n workflow with an AI Agent node connected to:

- **Model:** OpenAI chat model (GPT-5.4 Mini)
- **Memory:** Simple Memory
- **Tools:**
  - Marketstack: latest stock price, with the ticker chosen by the model
  - Google Sheets, get rows: reads the portfolio sheet
  - Google Sheets, append row: adds a trade, with ticker and share count chosen by the model

![Full workflow](images/01-full-workflow.png)

## Setup

- n8n account (free 14-day trial)
- OpenAI API key
- Marketstack API key (free tier)
- A Google Sheet called `Investments` with two rows: Amazon (10 shares) and Apple (2 shares)

## Steps

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

## Results

*(Fill in after running it: what the agent valued the portfolio at, which tickers and share counts it chose, and anything that surprised me.)*

![Final sheet](images/08-final-sheet.png)

## What I took from it

- The agent picks tools based on the descriptions written for them, so descriptions matter.
- Nothing is actually bought. The agent only writes rows to the sheet.
- Results differ run to run, since the model chooses its own tickers and quantities.

## Files

- [`workflow.json`](./workflow.json): exported n8n workflow (checked for secrets before committing)
