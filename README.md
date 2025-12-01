# converastional-ai-with-langraph
Competitor Analysis AI with LangGraph

This project implements a conversational AI agent designed to perform market research and generate competitor analysis reports. It utilizes a self-correcting retrieval-augmented generation (RAG) pipeline to ensure high-quality results.

The system uses LangGraph to manage the workflow, allowing the agent to search the web, evaluate the relevance of the findings, rewrite search queries if the initial results are poor, and synthesize a final report.

Features

    Real-time web search: uses DuckDuckGo to find up-to-date information on competitors, footfall trends, and peak hours.

    Self-correction: includes a feedback loop where the agent evaluates search results. If the data is found to be irrelevant or insufficient, the agent rewrites the search query and tries again.

    Quality control: a dedicated grading step ensures that only relevant data is passed to the final generation step.

    Structured reporting: generates professional business reports including key competitors, traffic analysis, and strategic recommendations.

Prerequisites

    Python 3.8 or higher

    An OpenAI API key

Installation

To install the required dependencies, run the following command:
Bash

pip install langgraph langchain langchain_openai langchain_community duckduckgo-search ddgs

Configuration

You must set your OpenAI API key as an environment variable or directly in the script before running the code.
Python

import os
os.environ["OPENAI_API_KEY"] = "your-actual-api-key-here"

Usage

The main script defines a state graph with several nodes. To run the analysis, execute the script. The default example query analyzes clothing store competitors in Koramangala, Bangalore.
Python

# Example input defined in the script
location_query = (
    "Analyze clothing store competitors in Koramangala, Bangalore. "
    "Find their names, footfall trends, and busiest hours."
)

The output will stream the progress of each node (agent decision, searching, grading, rewriting) and finally print the generated report.

Workflow architecture

The AI operates through a specific flow of nodes:

    Agent: the entry point that decides whether to perform a search based on the user's query.

    Search: executes a query using the DuckDuckGo search tool to gather information.

    Grade documents: evaluates the retrieved search results for relevance.

        If the data is good, the flow proceeds to the generation step.

        If the data is poor, the flow proceeds to the rewrite step.

    Rewrite: uses a large language model to formulate a more specific and effective search query based on the failed attempt, then loops back to the agent.

    Generate: synthesizes the validated search context into a final competitor analysis report.

Dependencies

    langgraph: for building the stateful, multi-actor application graph.

    langchain: for the overall framework and chain management.

    langchain_openai: for accessing GPT-4 and other OpenAI models.

    duckduckgo-search: for performing web searches.

    pydantic: for data validation and structure.
