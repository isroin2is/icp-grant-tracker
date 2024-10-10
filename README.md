# Overview

ICP Grant Tracker is designed to automatically assess the activity level of blockchain projects and determine if they can be considered "Active" or "Inactive". The agent assesses social media scores, github scores, and on-chain activity scores to determine how active the project is building so that the analysis can be further used as a criteria for the grant allocation.

# Problem

According to [Gitcoin’s State of the Web3 Grant Report](https://docs.google.com/document/d/1CFD6ztSh2ggJSO-U3uEea92UVB1cRbvBlA1tfPxLKi8/edit), there are over 1B $USD of grant issued across 5,900 projects in 2023. However, it lacks a standardized and automated measure to assess the activity of the project such that it requires extra effort for validation and the fund may be allocated to the wrong project.

# Solution

Dead Project Snipper offers an automated agent that

1. Collects data from the projects’ social(ex. X), building(ex. Github), and user(ex. onchain transaction) activity and store it on the activity database
2. Calculates the activity score based on the score calculator algorithm for “Dead” and “Active” analysis
3. Reports whether the project is dead or alive with the analysis data to back up the judgement. The report will be stored onchain for further verification

# System Architecture

![ICP Grant Tracker](https://github.com/isroin2is/icp-grant-tracker/blob/main/ICP%20Grant%20Tracker.png?raw=true)

### System Flow

The project consist of three main flows, which is coded alphabetically.

* Collect & organize data points: This means figuring out which project is the target for monitoring, and acquiring the project's social/github/wallet address. This part is less about programming; it's more about coordinating with funded projects for information.
* Collect activity data: Once data points are set, we use APIs to monitor and collect activity data in regular cycle.
* Judgement and action: Activity data is ingested to llm-based algorithm. Based on the result score, fact-based reports are created (by llm), actions may be called, and the info is updated to offchain DB & mainnet.

### Details

* Data point / Collector: Github / X Api collecter, ICP onchain data indexing
* Data Sets for the Metrics: Web3 Grant Funding DB (most likely to be Gitcoin but need discussion)
* Score Calculator: Multipath reasoning algorithm that utilizes LLM-as-a-judge
* Report: Instruction based prompt engineering with RAG on Langchain
* Report UI: Colab with metrics and instructions on how to customize them

# Impact

* Historical Grant Assessment: Check and see whether previous grant projects are still in progress or not
* Grant Project Management: Check the current grant projects to see if their activity should be eligible for the amount
* Grant Criteria Setup: Set up metrics for the least / preferred required activities for the grant recipient
