---
layout: page
title: Natural-Language Query Interface for NoSQL (NL → MongoDB)
permalink: /case-studies/nl-mongodb/
---

[← Back to Portfolio](/portfolio/)

# Natural-Language Query Interface for NoSQL (NL → MongoDB)

## Overview
**Context.** Most natural-language-to-database work targets SQL (~70%), while a smaller portion targets NoSQL (~15%). Meanwhile, modern datasets are often diverse, dynamic, and better served by flexible schemas. :contentReference[oaicite:7]{index=7}

**Goal.** Build a practical system that converts natural-language questions into **executable MongoDB queries**, supports **user-uploaded CSVs with varying schemas**, and shows **real-time results + logs** from multiple LLMs. :contentReference[oaicite:8]{index=8}

**Users.** Non-technical users, researchers, developers, and data analysts. :contentReference[oaicite:9]{index=9}

**Repository.**
- GitHub: https://github.com/enochakli/natural-language-queries-to-mongodb

- --
## Prototype UI (Find results)
![Prototype UI showing Find results.]({{ site.baseurl }}/assets/nl-mongodb/ui-find-results.png)


---

## What I Built / Key Features
- **Schema-agnostic workflow:** users can upload CSVs with different schemas and still query them via natural language. :contentReference[oaicite:10]{index=10}  
- **Multi-model support:** run the same prompt across multiple LLMs and compare outputs/logs. :contentReference[oaicite:11]{index=11}  
- **Real-time query execution + visualization:** translate NL → MongoDB query → execute → display results. :contentReference[oaicite:12]{index=12}  

---

## System Architecture (High-level)
**Backend:** Express.js REST API + MongoDB storage. :contentReference[oaicite:13]{index=13}  
**Frontend:** Angular + TypeScript, Angular Material, NgRx. :contentReference[oaicite:14]{index=14}  
**LLM Provider:** Groq API for high-speed inference. :contentReference[oaicite:15]{index=15}  
**Testing:** Postman for API testing and validation. :contentReference[oaicite:16]{index=16}  
## LLM system prompt (query translation)
![System prompt used to translate natural language into MongoDB JSON.]({{ site.baseurl }}/assets/nl-mongodb/system-prompt.png)


---

## Models & Datasets
**Models used:** Llama 3.1 8B, Llama 3.3 70B, GPT OSS 20B, GPT OSS 120B. :contentReference[oaicite:17]{index=17}  

**Datasets used for demos/testing:** Bike Store, NBA, Flight Routes, Roller Coasters, World Cities, European Soccer. :contentReference[oaicite:18]{index=18}  

---

## Prompting Strategy (Why outputs are executable)
We designed the system prompt to return **only a valid MongoDB query JSON** so the backend can execute it directly (no extra explanation text). :contentReference[oaicite:19]{index=19}

## Output stored as structured chat logs
![Example of stored chat logs showing user request and generated query.]({{ site.baseurl }}/assets/nl-mongodb/mongodb-compass-find-results.png)

---

## Evaluation Plan
We planned a **System Usability Scale (SUS)** post-test after users interact with the NL2NoSQL interface, then use feedback to improve usability. :contentReference[oaicite:20]{index=20}

---

## Technical Challenges & Future Improvements
**Challenges observed:** larger datasets took longer to upload (~10 minutes), LLM hallucinations, token limits. :contentReference[oaicite:21]{index=21}  
**Next steps:** add more LLMs, support dataset manipulation, improve injection mitigation, and evaluate generation quality systematically. :contentReference[oaicite:22]{index=22}  

---

## My Contributions
- (Fill this in with what *you* personally did: e.g., API routes, prompt design, UI work, testing, evaluation plan, writeup)
