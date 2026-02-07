---
layout: page
permalink: /case-studies/nl-mongodb/
---

[← Back to Portfolio]({{ site.baseurl }}/)

# Natural-Language Query Interface for NoSQL (NL → MongoDB)

A schema-agnostic web app that lets users upload datasets (CSV), ask questions in natural language, and receive executable MongoDB queries with real-time results while comparing outputs across multiple LLMs.

**Repository:** <a class="btn" href="https://github.com/enochakli/natural-language-queries-to-mongodb" target="_blank" rel="noopener">GitHub Repo</a>

---

## Snapshot

**Problem**
MongoDB querying is powerful, but it’s a barrier for people who don’t know NoSQL syntax especially when datasets vary widely in schema.

**Solution**
A workflow that translates natural language → valid MongoDB query JSON → executed results, with a UI that supports: 
- dataset upload (CSV)
- chat-based querying
- multi-model selection
- query logs + outputs

**Primary success criterion**
The system consistently generates valid, executable MongoDB queries across different schemas (rather than optimizing for benchmark scores).

---

## User Interface Walkthrough

### Entry and authentication
This is the app landing experience (login/sign-up).

![Landing page showing authentication screen.]({{ site.baseurl }}/assets/nl-mongodb/landing-page.png)

---

### Home screen and navigation
After login, users can create/select chats and begin querying.

![Homepage showing chat list and main workspace.]({{ site.baseurl }}/assets/nl-mongodb/homepage.png)

---

### Start a new session by uploading a dataset
Users upload a CSV to initialize a chat session tied to a dataset.

![New chat view with CSV upload card.]({{ site.baseurl }}/assets/nl-mongodb/new-chat-view.png)

---

### Querying in chat and viewing results
Users ask a question in natural language; the app generates a MongoDB query and displays results.

![Chat view showing a natural-language question and returned results.]({{ site.baseurl }}/assets/nl-mongodb/chat-view.png)

---

### Manage chat sessions (rename/delete)
This supports organization and makes the workflow usable across multiple datasets/topics.

![Chat action menu showing rename and delete options.]({{ site.baseurl }}/assets/nl-mongodb/chat-action-menu.png)

---

### Key features
- **Schema-agnostic workflow:** users upload different CSVs and still query without manually learning schema-specific syntax.
- **Multi-model support:** users can run the same prompt using different LLMs to compare outputs and reliability.
- **Executable output constraint:** system prompt forces LLM to return only valid MongoDB query JSON to reduce parsing failures.
- **Real-time execution:** generated query is executed immediately and results render inside the app.

---

## Prompting Strategy

A core design decision was constraining the model output so the system remains reliable and executable.

**Approach**
- Provide a dataset sample to ground the model
- Require the model to return only valid MongoDB “find query” JSON
- Avoid extra prose that breaks execution

![System prompt used to translate NL requests into MongoDB query JSON.]({{ site.baseurl }}/assets/nl-mongodb/system-prompt.png)

---

## Technical Architecture

**Frontend**
- Angular and TypeScript
- User interface built with Material-style components and a chat-based layout

**Backend**
- Express.js REST API
- MongoDB for persistence (documents + chat/query logs)

**LLM execution**
- Groq API for fast inference and rapid iteration across models

**Testing**
- Postman to validate API endpoints and verify query execution behavior

---

## Data and Model Coverage

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
We intend to use this because the goal was usability for non-experts, we prioritized measuring perceived usability and collecting feedback to guide user interface improvements.

![System Usability Scale (SUS) questionnaire used for post-test evaluation.]({{ site.baseurl }}/assets/nl-mongodb/system-usability-scale-questionnaire.png)

### Planned evaluation steps
1. Recruit participants with varied technical backgrounds  
2. Introduce the system and workflow (upload CSV → ask questions → review results)  
3. Run predefined tasks (upload dataset, query, review output, iterate)  
4. Observe interaction patterns + note confusion points / errors  
5. Administer SUS post-test questionnaire  
6. Collect open-ended feedback (what worked / what was confusing)  
7. Analyze SUS scores and qualitative comments to determine improvements  

---

## Technical Challenges

** Hallucinated query structure**
The system rarely hallucinates data values, but it sometimes hallucinates:
- field names / schema assumptions
- query operators or nesting patterns

** Dataset upload latency**
Large datasets can take significant time to upload (~10 minutes in some cases), which hurts UX.

** Token and context limits**
Providing schema hints and samples helps reliability, but longer context increases costs and can still fail on edge cases.

---

## Recommendations and Future Improvements

**Production readiness**
- add configuration management (environment consistency, deployment workflow)
- handle API reliability and rate-limits for LLM providers
- improve performance for large dataset uploads
- harden frontend to backend communication for real-world load

**Query reliability**
- add schema extraction + automatic field validation before execution
- add query repair loop (detect failure → ask model to fix JSON)
- improve injection mitigation and safer execution constraints

**Evaluation**
- prioritize completing the planned SUS study to validate usability
- use results to guide user interface changes (onboarding, error feedback, transparency)

---

## MongoDB - DBMS choice 

MongoDB stores data in flexible JSON-like documents, which makes it strong for:
- semi-structured datasets
- varying schemas across uploads
- scalable, high-performance querying in many industry contexts

For this project, MongoDB was a good fit because the system needed to support many different dataset structures without migrations.

---

## My Contributions

- Shaped the core research problem and end-to-end project scope for translating natural language questions into executable MongoDB queries.
- Led the literature review effort by sourcing, comparing, and synthesizing prior NL2DB/NL2NoSQL research to justify design choices.
- Designed the user evaluation methodology, including participant plan, task flow, interaction logging strategy, and success measures aligned with usability goals.
- Authored the usability testing approach and built the SUS post-test questionnaire used to capture perceived usability and user satisfaction.
- Contributed to the final report writing and organization, ensuring the narrative clearly communicated goals, methods, results, limitations, and next steps.
