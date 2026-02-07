---
layout: page
title: Natural-Language Query Interface for NoSQL (NL → MongoDB)
permalink: /case-studies/nl-mongodb/
---

[← Back to Portfolio](/portfolio/)

# Natural-Language Query Interface for NoSQL (NL → MongoDB)

## Overview
**Context.** Most natural-language-to-database work targets SQL (~70%), while a smaller portion targets NoSQL (~15%). Meanwhile, modern datasets are often diverse, dynamic, and better served by flexible schemas. 

**Goal.** Build a practical system that converts natural-language questions into **executable MongoDB queries**, supports **user-uploaded CSVs with varying schemas**, and shows **real-time results + logs** from multiple LLMs. 

**Users.** Non-technical users, researchers, developers, and data analysts. 

**Repository.**
- GitHub: https://github.com/enochakli/natural-language-queries-to-mongodb

## Prototype UI (Find results)
![Prototype UI showing Find results.](/portfolio/assets/nl-mongodb/ui-find-results.png)


---

## What I Built / Key Features
- **Schema-agnostic workflow:** users can upload CSVs with different schemas and still query them via natural language.  
- **Multi-model support:** run the same prompt across multiple LLMs and compare outputs/logs.  
- **Real-time query execution + visualization:** translate NL → MongoDB query → execute → display results. 

---

## System Architecture (High-level)
**Backend:** Express.js REST API + MongoDB storage.
**Frontend:** Angular + TypeScript, Angular Material, NgRx.
**LLM Provider:** Groq API for high-speed inference.
**Testing:** Postman for API testing and validation.   

## LLM system prompt (query translation)
![System prompt used to translate natural language into MongoDB JSON.](/portfolio/assets/nl-mongodb/system-prompt.png)


---

## Models & Datasets
**Models used:** Llama 3.1 8B, Llama 3.3 70B, GPT OSS 20B, GPT OSS 120B. 
**Datasets used for demos/testing:** Bike Store, NBA, Flight Routes, Roller Coasters, World Cities, European Soccer. 

---

## Prompting Strategy (Why outputs are executable)
We designed the system prompt to return **only a valid MongoDB query JSON** so the backend can execute it directly (no extra explanation text).

## Output stored as structured chat logs
![Example of stored chat logs showing user request and generated query.](/portfolio/assets/nl-mongodb/mongodb-compass-find-results.png)

---

## Evaluation Plan
We planned a **System Usability Scale (SUS)** post-test after users interact with the NL2NoSQL interface, then use feedback to improve usability. 

---

## Technical Challenges & Future Improvements
**Challenges observed:** larger datasets took longer to upload (~10 minutes), LLM hallucinations, token limits. 
**Next steps:** add more LLMs, support dataset manipulation, improve injection mitigation, and evaluate generation quality systematically. 

---

## My Contributions
- (Fill this in with what *you* personally did: e.g., API routes, prompt design, UI work, testing, evaluation plan, writeup)
