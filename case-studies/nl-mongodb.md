---
layout: page
permalink: /case-studies/nl-mongodb/
---

[← Back to Portfolio]({{ site.baseurl }}/)

# Natural-Language Query Interface for NoSQL (NL → MongoDB)

A schema-agnostic web app that lets users upload datasets (CSV), ask questions in natural language, and receive **executable MongoDB queries** with **real-time results**—while comparing outputs across multiple LLMs.

**Repository:** <a class="btn" href="https://github.com/enochakli/natural-language-queries-to-mongodb" target="_blank" rel="noopener">GitHub Repo</a>

---

## Snapshot

**Problem**
MongoDB querying is powerful, but it’s a barrier for people who don’t know NoSQL syntax—especially when datasets vary widely in schema.

**Solution**
A workflow that translates **natural language → valid MongoDB query JSON → executed results**, with a UI that supports: 
- dataset upload (CSV)
- chat-based querying
- multi-model selection
- query logs + outputs

**Primary success criterion**
The system consistently generates **valid, executable MongoDB queries** across different schemas (rather than optimizing for benchmark scores).

---

## UI Walkthrough

### 1) Entry + authentication
This is the app landing experience (login/sign-up).

![Landing page showing authentication screen.]({{ site.baseurl }}/assets/nl-mongodb/landing-page.png)

---

### 2) Home screen and navigation
After login, users can create/select chats and begin querying.

![Homepage showing chat list and main workspace.]({{ site.baseurl }}/assets/nl-mongodb/homepage.png)

---

### 3) Start a new session by uploading a dataset
Users upload a CSV to initialize a chat session tied to a dataset.

![New chat view with CSV upload card.]({{ site.baseurl }}/assets/nl-mongodb/new-chat-view.png)

---

### 4) Querying in chat + viewing results
Users ask a question in natural language; the app generates a MongoDB query and displays results.

![Chat view showing a natural-language question and returned results.]({{ site.baseurl }}/assets/nl-mongodb/chat-view.png)

---

### 5) Manage chat sessions (rename/delete)
This supports organization and makes the workflow usable across multiple datasets/topics.

![Chat action menu showing rename and delete options.]({{ site.baseurl }}/assets/nl-mongodb/chat-action-menu.png)

---

## What I Built

### Key features
- **Schema-agnostic workflow:** users upload different CSVs and still query without manually learning schema-specific syntax.
- **Multi-model support:** users can run the same prompt using different LLMs to compare outputs and reliability.
- **Executable output constraint:** system prompt forces LLM to return *only valid MongoDB query JSON* to reduce parsing failures.
- **Real-time execution:** generated query is executed immediately and results render inside the app.

---

## Prompting Strategy

A core design decision was constraining the model output so the system remains **reliable and executable**.

**Approach**
- Provide a **dataset sample** to ground the model
- Require the model to return **only valid MongoDB “find query” JSON**
- Avoid extra prose that breaks execution

![System prompt used to translate NL requests into MongoDB query JSON.]({{ site.baseurl }}/assets/nl-mongodb/system-prompt.png)

---

## Technical Architecture

**Frontend**
- Angular + TypeScript
- UI built with Material-style components and a chat-based layout

**Backend**
- Express.js REST API
- MongoDB for persistence (documents + chat/query logs)

**LLM execution**
- Groq API for fast inference and rapid iteration across models

**Testing**
- Postman to validate API endpoints and verify query execution behavior

---

## Data + Model Coverage

**Models used**
- Llama 3.1 8B
- Llama 3.3 70B
- GPT OSS 20B
- GPT OSS 120B

**Datasets used for demos/testing**
- Bike Store
- NBA
- Flight Routes
- Roller Coasters
- World Cities
- European Soccer

---

## Evaluation Plan (Planned, Not Yet Completed)

We planned a usability-focused evaluation using the **System Usability Scale (SUS)** to measure perceived ease of use and satisfaction after interacting with the system.

**Why SUS**
Because the goal was usability for non-experts, we prioritized measuring *perceived usability* and collecting feedback to guide UI improvements.

![System Usability Scale (SUS) questionnaire used for post-test evaluation.]({{ site.baseurl }}/assets/nl-mongodb/system-usability-scale-questionnaire.png)

### Planned evaluation steps
1. Recruit participants with varied technical backgrounds  
2. Introduce the system and workflow (upload CSV → ask questions → review results)  
3. Run predefined tasks (upload dataset, query, review output, iterate)  
4. Observe interaction patterns + note confusion points / errors  
5. Administer SUS post-test questionnaire  
6. Collect open-ended feedback (what worked / what was confusing)  
7. Analyze SUS scores + qualitative comments to determine improvements  

---

## Technical Challenges

**1) Hallucinated query structure**
The system rarely hallucinates data values, but it sometimes hallucinates:
- field names / schema assumptions
- query operators or nesting patterns

**2) Dataset upload latency**
Large datasets can take significant time to upload (~10 minutes in some cases), which hurts UX.

**3) Token and context limits**
Providing schema hints and samples helps reliability, but longer context increases costs and can still fail on edge cases.

---

## Recommendations and Future Improvements

**Production readiness**
- add configuration management (environment consistency, deployment workflow)
- handle API reliability and rate-limits for LLM providers
- improve performance for large dataset uploads
- harden frontend ↔ backend communication for real-world load

**Query reliability**
- add schema extraction + automatic field validation before execution
- add query repair loop (detect failure → ask model to fix JSON)
- improve injection mitigation and safer execution constraints

**Evaluation**
- prioritize completing the planned SUS study to validate usability
- use results to guide UI changes (onboarding, error feedback, transparency)

---

## Why MongoDB (DBMS choice)

MongoDB stores data in flexible JSON-like documents, which makes it strong for:
- semi-structured datasets
- varying schemas across uploads
- scalable, high-performance querying in many industry contexts

For this project, MongoDB was a good fit because the system needed to support **many different dataset structures without migrations**.

---

## My Contributions
*(Replace this with what you personally did.)*

Examples you can include:
- Designed the end-to-end workflow (CSV upload → schema sample → prompt → execution → results UI)
- Implemented API routes for query execution + dataset handling
- Built the chat interface and chat management actions
- Designed the system prompt for executable query-only output
- Created the evaluation plan and SUS questionnaire workflow
