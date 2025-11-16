# Debate Simulation System 

This project implements a multi-agent debate simulation system. Two agents — a Scientist and a Philosopher — debate a user-provided topic in multiple rounds. The system keeps track of arguments, uses semantic similarity to judge relevance, and produces a DAG visualization showing the debate flow.

# Features

Multi-round debate between two AI agents using Google Gemini API.

Maintains a memory of arguments for context-aware responses.

Semantic evaluation of arguments using Sentence Transformers.

Automatic winner selection based on relevance to the topic.

Generates a DAG visualization of the debate flow.

Saves a log file of all rounds, summary, and winner.

# Installation
1. Clone the repository
git clone <repository_url>
cd <repository_folder>

2. Install dependencies
pip install google-genai sentence-transformers graphviz

3. Environment Setup

Set your Google Gemini API key as an environment variable:

import os
os.environ["GEMINI_API_KEY"] = "YOUR_GOOGLE_GEMINI_API_KEY"

# Running the Program

Run the script using Python:

python debate_simulation.py


The program will ask you to enter a debate topic.

The debate will run for 8 rounds, alternating between the Scientist and the Philosopher.

After each round:

The argument of the current agent is displayed.

Arguments are stored in memory for future rounds.

Once all rounds are complete:

A debate summary is printed.

The winner is determined based on semantic relevance to the topic.

A DAG visualization of the debate flow is generated and saved as debate_dag.png.

A log file of the debate is saved in the working directory, e.g., debate_log_20251116_123456.txt.

# Node & DAG Structure

The debate is modeled as a Directed Acyclic Graph (DAG):

Nodes:

UserInput

The node where the user provides the debate topic.

Sends the topic to both agents.

AgentA (Scientist)

Generates arguments from a scientific perspective.

Receives memory from previous rounds for context.

AgentB (Philosopher)

Generates arguments from a philosophical perspective.

Receives memory from previous rounds for context.

Memory

Stores all arguments from both agents.

Feeds back to agents for context-aware reasoning.

Provides all arguments to the Judge.

Judge

Evaluates all arguments using semantic similarity with the debate topic.

Determines the winner and provides a reasoning explanation.

Edges:

UserInput → AgentA

UserInput → AgentB

AgentA → Memory

AgentB → Memory

Memory → AgentA

Memory → AgentB

Memory → Judge

This ensures:

Topic is shared with both agents.

Memory maintains context for multi-round debates.

Judge evaluates the full transcript to determine relevance.

# DAG Visualization

The system generates a graphical representation of the debate flow using Graphviz. Example structure:

UserInput
   │
   ├──> AgentA
   │      │
   │      └──> Memory
   │
   └──> AgentB
          │
          └──> Memory
Memory ─────> Judge


UserInput feeds both agents.

Memory aggregates all arguments and informs agents in subsequent rounds.

Judge uses the complete memory to determine the winner.

The DAG is saved as debate_dag.png.

# Log File

The program generates a log file with the following structure:

[Round 1] Scientist: <argument>
[Round 2] Philosopher: <argument>
...
[Judge] Summary:
<Debate summary text>
Winner: <Agent>
Reason: <semantic relevance scores>

# Notes

Ensure your Google Gemini API key is valid.

The system requires an internet connection to generate arguments using Gemini.

You can modify:

Number of rounds (range(8) in run_debate()).

Agent names or roles.


Semantic model (all-mpnet-base-v2) for scoring.
