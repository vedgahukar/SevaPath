
# 🇮🇳 SevaPath

### **From Government Information to Verified Action**

**An evidence-grounded open-source AI system that transforms complex
government notifications into personalized, explainable and actionable
opportunities.**

![Status](https://img.shields.io/badge/status-qualifier%20proposal-blue)
![Hackathon](https://img.shields.io/badge/Hacktober%20Fest-Open%20Source%20AI%20Hackathon-orange)
![AI](https://img.shields.io/badge/AI-Gemma%204%20%7C%20RAG-purple)
![License](https://img.shields.io/badge/license-to%20be%20defined-lightgrey)
:::

> **Hackathon MVP:** Upload one official government notification PDF →
> understand the opportunity → extract and verify eligibility, dates,
> fees and required documents → match the opportunity against a user
> profile → explain the result with source evidence → generate an
> actionable next-step plan → provide the official application/source
> link when available.

> **Qualifier scope:** This repository contains only the technical
> proposal. Implementation code, datasets, notebooks, binaries and
> generated implementation files are not part of the qualifier
> submission.

------------------------------------------------------------------------

## Table of Contents

1.  [Project Name](#1-project-name)
2.  [Problem Statement](#2-problem-statement)
3.  [Project Overview](#3-project-overview)
4.  [Proposed Solution](#4-proposed-solution)
5.  [Objectives](#5-objectives)
6.  [Target Users / Use Case](#6-target-users--use-case)
7.  [Open-Source AI Technology
    Selected](#7-open-source-ai-technology-selected)
8.  [Why This Technology Was
    Selected](#8-why-this-technology-was-selected)
9.  [AI's Role in the System](#9-ais-role-in-the-system)
10. [System Architecture](#10-system-architecture)
11. [Component-Level Architecture](#11-component-level-architecture)
12. [Data / Information Flow](#12-data--information-flow)
13. [Agentic Workflow](#13-agentic-workflow)
14. [Technology Stack](#14-technology-stack)
15. [Expected Features](#15-expected-features)
16. [Implementation Approach](#16-implementation-approach)
17. [Expected Final Output](#17-expected-final-output)
18. [Future Scope / Scalability](#18-future-scope--scalability)
19. [Open-Source Dependencies /
    Components](#19-open-source-dependencies--components)
20. [Expected Challenges and
    Mitigation](#20-expected-challenges-and-mitigation)
21. [Evaluation Strategy](#21-evaluation-strategy)
22. [Responsible AI and Government-Information
    Safety](#22-responsible-ai-and-government-information-safety)
23. [Hackathon Scope](#23-hackathon-scope)

------------------------------------------------------------------------

# 1. Project Name

## SevaPath

### **From Government Information to Verified Action**

**Tagline:** *Turning complex government notifications into clear,
personalized and actionable opportunities.*

SevaPath is an open-source AI-powered Government Opportunity
Intelligence Engine designed to help people understand government
notifications and determine what those opportunities mean for them.

The system focuses on scholarships, recruitment notifications,
apprenticeships, welfare schemes, subsidies, educational grants and
similar government opportunities.

------------------------------------------------------------------------

# 2. Problem Statement

Every year, students, graduates, job seekers and citizens receive access
to government opportunities through official portals, circulars,
recruitment notifications, scheme documents and long PDF notices.

The problem is not simply a lack of information.

The problem is that people often cannot understand, discover or track
the opportunities that are relevant to them.

### Why do people miss opportunities?

1.  **Information is scattered**
    -   Different departments and organizations publish opportunities on
        different websites and portals.
2.  **Official notifications are difficult to understand**
    -   A single notification can contain many pages of eligibility
        rules, exceptions, dates, fees, category conditions and document
        requirements.
3.  **Eligibility is difficult to check manually**
    -   Users may need to compare age, qualification, state, category,
        income, marks, course, experience and other conditions.
4.  **Deadlines are easy to miss**
    -   Important dates may be buried inside long documents or changed
        through later notifications.
5.  **Required documents are not always obvious**
    -   Applicants may discover missing certificates only when they
        begin the application process.
6.  **Unofficial summaries can be unreliable**
    -   Simplification is useful only when it remains connected to the
        original official source.

### Core problem

A user may read a 20--50 page government notification and still not
know:

> **"Am I eligible, what do I need, when is the deadline, where do I
> apply, and what should I do next?"**

SevaPath addresses this problem while keeping the **official
notification as the source of truth**.

------------------------------------------------------------------------

# 3. Project Overview

SevaPath converts complex government notifications into a structured,
searchable, evidence-backed and personalized opportunity guide.

### Input

-   Official government notification PDF
-   Scanned/image-based PDF
-   User profile
-   Natural-language questions

### Processing

``` text
Government Notification
        ↓
Document Processing
        ↓
OCR / Text Extraction
        ↓
Page & Section Preservation
        ↓
Chunking + Metadata
        ↓
Embeddings / Vector Search
        ↓
Evidence Retrieval
        ↓
Open-Source AI Reasoning
        ↓
Structured Opportunity Information
        ↓
Eligibility Reasoning
        ↓
Evidence Verification
        ↓
Personalized Matching
        ↓
Action Planning
```

### Output

``` text
Opportunity Summary
+ Eligibility Result
+ Eligibility Reasoning
+ Evidence / Page Reference
+ Required Documents
+ Deadline
+ Uncertainty / Verification Status
+ Action Plan
+ Official Application / Source Link
```

### Core principle

> **The AI explains the document; it does not replace the document.**

Important claims should remain connected to retrieved source content so
that users can inspect where the information came from.

------------------------------------------------------------------------

# 4. Proposed Solution

SevaPath treats government-notification understanding as a **retrieval,
structured reasoning and verification problem**, rather than simply a
chatbot problem.

## 4.1 Document Intelligence

The system accepts official government notifications and processes both
digital and scanned documents.

It extracts and structures:

-   Opportunity title
-   Issuing organization
-   Application start date
-   Application closing date
-   Eligibility criteria
-   Age requirements
-   Educational qualification
-   Category requirements
-   Income conditions
-   State/residence conditions
-   Application fee
-   Required documents
-   Selection/process information
-   Official application/source link
-   Page-level source references

------------------------------------------------------------------------

## 4.2 Evidence-Grounded Retrieval

Instead of asking the model to reason over an entire document blindly,
SevaPath retrieves the most relevant source sections.

``` text
User Question
      ↓
Question Embedding
      ↓
Semantic Search
      ↓
Relevant Notification Chunks
      ↓
Page-Level Evidence
      ↓
Open-Source LLM
      ↓
Answer + Evidence
```

If reliable evidence cannot be found, the system should return:

> **"Not found in the provided notification."**

It should not manufacture an answer.

------------------------------------------------------------------------

## 4.3 Structured Opportunity Knowledge

Important information is stored as structured data instead of relying
only on generated prose.

Example:

``` json
{
  "title": "Example Scholarship",
  "organization": "Example Department",
  "category": "Scholarship",
  "application_start": "YYYY-MM-DD",
  "application_deadline": "YYYY-MM-DD",
  "eligibility": {
    "minimum_age": null,
    "maximum_age": 25,
    "qualification": "Undergraduate student",
    "category": ["SC", "ST", "OBC"],
    "income_limit": 250000,
    "state": "Maharashtra"
  },
  "documents": [
    "Income Certificate",
    "Domicile Certificate",
    "Marksheet"
  ],
  "official_link": "source link if present",
  "source_pages": [2, 5, 7]
}
```

Values not present in the source remain **unknown/null** instead of
being guessed.

------------------------------------------------------------------------

## 4.4 Eligibility Reasoning Engine

SevaPath compares the user's profile against explicit requirements.

Example:

``` text
User Profile
────────────
Age: 19
State: Maharashtra
Qualification: B.Tech
Category: OBC
Income: ₹1,00,000

Notification Requirements
──────────────────────────
Age: ≤ 25
Qualification: Undergraduate
Category: SC/ST/OBC
Income: ≤ ₹2,50,000
State: Maharashtra
```

Result:

``` text
🟢 LIKELY ELIGIBLE

✓ Age condition satisfied
✓ Qualification condition satisfied
✓ Category condition satisfied
✓ Income condition satisfied
✓ State condition satisfied
```

The system does not claim official approval. It explains whether the
provided profile appears to satisfy the conditions stated in the
notification.

------------------------------------------------------------------------

## 4.5 Eligibility Reasoning Graph

A major differentiating feature is an explainable eligibility graph.

``` text
                 OPPORTUNITY
                      │
        ┌─────────────┼─────────────┐
        ↓             ↓             ↓
       AGE       QUALIFICATION    INCOME
        ✓             ✓             ✓
        │             │             │
        └─────────────┼─────────────┘
                      ↓
                  CATEGORY
                      ✓
                      ↓
               STATE / DOMICILE
                      ✓
                      ↓
              ELIGIBILITY RESULT
```

Each condition can retain:

-   User-provided value
-   Required value
-   Comparison result
-   Source page
-   Evidence
-   Confidence
-   Verification state

This makes the result explainable rather than a black-box prediction.

------------------------------------------------------------------------

## 4.6 Uncertainty and Verification Engine

SevaPath should not force every case into a binary answer.

### 🟢 Likely Eligible

Known conditions are satisfied.

### 🔴 Likely Not Eligible

An explicit condition is not satisfied.

### 🟡 Needs Verification

A requirement is ambiguous, conditional, missing or difficult to
interpret.

### ⚠ Contradiction Detected

Conflicting information is detected within the document or across
notification versions.

This allows the system to communicate uncertainty instead of creating
false confidence.

------------------------------------------------------------------------

## 4.7 Contradiction Detection

Government notifications may contain:

-   general conditions
-   category-specific exceptions
-   multiple dates
-   amendments
-   revised instructions

SevaPath can identify potentially conflicting information.

Example:

``` text
⚠ CONTRADICTION / EXCEPTION

General maximum age:
25 years

Special category:
27 years

Applicable to:
Specified category

Evidence:
Page 4
Page 11
```

The system should surface the conflict and request verification rather
than silently choosing one interpretation.

------------------------------------------------------------------------

## 4.8 Notification Change Detection

When multiple versions of a notification are available, SevaPath can
compare them.

Example:

``` text
NOTIFICATION UPDATE DETECTED

Previous deadline:
15 October

New deadline:
25 October

Changed field:
Application deadline

Source:
Amendment Notification
```

This allows users to identify important changes without manually
comparing long documents.

------------------------------------------------------------------------

## 4.9 Personalized Action Plan

The final output should not stop at eligibility.

Example:

``` text
APPLICATION PLAN

✓ Eligibility checked
✓ Marksheet available
⚠ Income Certificate required
⚠ Domicile verification required

NEXT STEPS

1. Obtain income certificate
2. Prepare domicile certificate
3. Prepare required academic documents
4. Visit the official application portal
5. Submit before the deadline
```

The goal is:

> **Information → Understanding → Decision → Action**

------------------------------------------------------------------------

# 5. Objectives

## Primary Objectives

1.  Process official government notification PDFs.
2.  Extract structured opportunity information.
3.  Retrieve evidence relevant to user questions.
4.  Use open-source AI as a core reasoning component.
5.  Extract and interpret eligibility conditions.
6.  Match user profiles against explicit requirements.
7.  Provide evidence-backed eligibility explanations.
8.  Identify missing, ambiguous or uncertain information.
9.  Generate required-document checklists.
10. Display application deadlines.
11. Detect important notification changes where multiple versions are
    provided.
12. Provide simple English and at least one Indian-language explanation
    mode.

## Secondary Objectives

-   Detect potentially conflicting information.
-   Distinguish "likely eligible", "likely not eligible" and "needs
    verification".
-   Refuse unsupported questions instead of guessing.
-   Provide an action-oriented deadline view.
-   Make the architecture reusable across scholarships, recruitment,
    apprenticeships and welfare schemes.

------------------------------------------------------------------------

# 6. Target Users / Use Case

  -----------------------------------------------------------------------
  User                                Need
  ----------------------------------- -----------------------------------
  **College students**                Scholarships, internships,
                                      apprenticeships and educational
                                      opportunities

  **Job seekers**                     Recruitment notifications,
                                      eligibility, fees and deadlines

  **Rural / first-generation          Understand complex official
  applicants**                        information

  **Economically weaker applicants**  Discover relevant scholarships and
                                      grants

  **Graduates**                       Government recruitment and
                                      apprenticeship opportunities

  **General citizens**                Understand welfare schemes and
                                      subsidies

  **College student cells**           Help students identify and
                                      understand opportunities
  -----------------------------------------------------------------------

## Primary Use Case

A second-year engineering student receives a 25-page government
scholarship notification.

Instead of reading the entire document manually, the student:

1.  Uploads the notification.
2.  Enters their profile.
3.  SevaPath extracts the opportunity requirements.
4.  The system compares the profile with the requirements.
5.  The user sees which conditions are satisfied.
6.  The system identifies missing documents.
7.  The user sees the deadline.
8.  Every important result can be traced to the official notification.
9.  The user receives a clear action plan.

## Example Questions

``` text
"Am I eligible for this scholarship?"

"What is the last date?"

"How much family income is allowed?"

"Is OBC category eligible?"

"What documents do I need?"

"Where do I apply?"

"Explain this notification in Marathi."

"Which condition is preventing me from being eligible?"
```

------------------------------------------------------------------------

# 7. Open-Source AI Technology Selected

  -----------------------------------------------------------------------
  Role                    Selected Technology     Purpose
  ----------------------- ----------------------- -----------------------
  **Core reasoning**      Gemma 4                 Government-document
                                                  reasoning, structured
                                                  extraction and
                                                  explanations

  **Semantic retrieval**  BGE-M3 or suitable      Semantic and
                          multilingual embedding  multilingual search
                          model                   

  **OCR**                 Tesseract or suitable   Scanned/image-based
                          open-source OCR         document processing

  **Vector search**       FAISS                   Retrieval of relevant
                                                  notification sections

  **PDF extraction**      PyMuPDF                 Extract text while
                                                  preserving page
                                                  information

  **Schema validation**   Pydantic                Validate structured AI
                                                  output

  **UI**                  Streamlit               Rapid interactive
                                                  application

  **Runtime**             Python                  AI/document processing
                                                  and orchestration
  -----------------------------------------------------------------------

The exact model/checkpoint should be finalized after testing against the
available hackathon hardware and representative notification documents.

------------------------------------------------------------------------

# 8. Why This Technology Was Selected

SevaPath has several requirements that make a basic chatbot
insufficient.

  -----------------------------------------------------------------------
  Requirement             Why It Matters          Proposed Approach
  ----------------------- ----------------------- -----------------------
  Long documents          Important information   Chunking + retrieval
                          can be spread across    
                          many pages              

  Reliable answers        Wrong dates or          RAG + evidence
                          eligibility conditions  
                          can harm applicants     

  Structured information  Users need dates, fees, Structured output
                          age and documents       
                          separately              

  Semantic search         User wording may differ Embeddings
                          from notification       
                          wording                 

  Multilingual support    Users may ask in Indian Multilingual retrieval
                          languages               

  Local / low-cost        Reduces unnecessary     Open-weight model
  inference               hosted API dependency   

  Page-level evidence     Claims must be          Page metadata
                          inspectable             

  Complex interpretation  Eligibility clauses can Gemma 4 reasoning
                          contain                 
                          conditions/exceptions   

  Uncertainty             AI should not invent    Verification layer
                          missing information     
  -----------------------------------------------------------------------

### Why not a normal chatbot?

A generic chatbot may:

-   ignore relevant parts of a long document
-   invent a deadline
-   confuse eligibility conditions
-   mix information from unrelated sections
-   provide no evidence
-   sound confident when evidence is weak

SevaPath therefore follows:

> **Retrieval first, reasoning second, verification before action.**

------------------------------------------------------------------------

# 9. AI's Role in the System

AI is a core component rather than an optional add-on.

  -----------------------------------------------------------------------
  Task                    Approach                Output
  ----------------------- ----------------------- -----------------------
  Document understanding  Gemma 4                 Structured
                                                  interpretation

  Semantic retrieval      Embeddings + FAISS      Relevant evidence

  Eligibility extraction  Gemma 4                 Requirements

  Deadline extraction     LLM + deterministic     Dates
                          validation              

  Document extraction     Gemma 4                 Checklist

  Question answering      RAG + Gemma 4           Evidence-grounded
                                                  answer

  Profile matching        Rules + AI              Match / mismatch /
                          interpretation          verification

  Explanation             Gemma 4                 Simple-language
                                                  explanation

  Regional explanation    Gemma 4                 Hindi / Marathi / other
                                                  supported language

  Contradiction detection AI + deterministic      Conflict/exception
                          comparison              

  Change detection        Structured comparison   Changed fields
  -----------------------------------------------------------------------

### AI vs deterministic logic

Not every task needs an LLM.

``` text
PDF extraction          → Deterministic
Page numbering          → Deterministic
Vector similarity       → Deterministic
Date calculations       → Deterministic
Schema validation       → Deterministic
Eligibility rules       → Deterministic where explicit
Complex clause meaning  → Gemma 4
Semantic QA             → Gemma 4
Explanation             → Gemma 4
Evidence interpretation → Gemma 4 + verification
```

This separation improves reliability and makes the system easier to
test.

------------------------------------------------------------------------

# 10. System Architecture

``` mermaid
flowchart TB

    subgraph INPUT["1. Input"]
        U["User"]
        PDF["Government Notification PDF"]
        PROFILE["User Profile"]
    end

    subgraph PRE["2. Document Processing"]
        P1["PDF Parser"]
        P2["OCR Fallback"]
        P3["Page + Section Processor"]
        P4["Metadata Extractor"]
    end

    subgraph RET["3. Retrieval Layer"]
        E["Embedding Model"]
        DB[("FAISS Vector Index")]
        R["Evidence Retriever"]
    end

    subgraph AI["4. Open-Source AI Layer"]
        LLM["Gemma 4"]
        S1["Opportunity Extraction"]
        S2["Eligibility Interpretation"]
        S3["Deadline / Fee Extraction"]
        S4["Document Checklist"]
        S5["Question Answering"]
        S6["Plain Language / Translation"]
    end

    subgraph INT["5. Intelligence Layer"]
        M1["Eligibility Rule Engine"]
        M2["Profile Matcher"]
        M3["Eligibility Reasoning Graph"]
        M4["Evidence Validator"]
        M5["Contradiction Detector"]
        M6["Change Detector"]
        M7["Confidence / Verification"]
        M8["Action Planner"]
    end

    subgraph OUTPUT["6. Output"]
        O1["Opportunity Summary"]
        O2["Eligibility Result"]
        O3["Reasoning Graph"]
        O4["Document Checklist"]
        O5["Deadline"]
        O6["Action Plan"]
        O7["Official Link"]
        O8["Source / Page Evidence"]
    end

    PDF --> P1
    P1 -->|"Digital PDF"| P3
    P1 -->|"Scanned PDF"| P2 --> P3
    P3 --> P4
    P4 --> E
    E --> DB
    DB --> R

    U --> PROFILE
    U -->|"Question"| R
    R --> LLM

    LLM --> S1
    LLM --> S2
    LLM --> S3
    LLM --> S4
    LLM --> S5
    LLM --> S6

    S2 --> M1
    M1 --> M2
    M2 --> M3
    S1 --> M3
    S2 --> M4
    R --> M4
    S1 --> M5
    S1 --> M6
    M4 --> M7
    M5 --> M7
    M6 --> M7
    M7 --> M8
    PROFILE --> M2

    S1 --> O1
    M7 --> O2
    M3 --> O3
    S4 --> O4
    S3 --> O5
    M8 --> O6
    P4 --> O7
    M4 --> O8
```

### Architecture principle

> **Retrieval finds evidence. AI interprets evidence. Deterministic
> logic validates explicit conditions. The verification layer decides
> whether the result is trustworthy enough to show as a confident
> result.**

------------------------------------------------------------------------

# 11. Component-Level Architecture

  ---------------------------------------------------------------------------
  \#                Component         Responsibility    Input → Output
  ----------------- ----------------- ----------------- ---------------------
  1                 Document          Accept official   PDF → document
                    Ingestion         notification      

  2                 PDF Parser        Extract digital   PDF → page text
                                      text              

  3                 OCR Engine        Process scanned   Image → text
                                      pages             

  4                 Page/Section      Preserve          Text → sections
                    Processor         boundaries        

  5                 Metadata          Identify title,   Document → metadata
                    Extractor         organization,     
                                      dates and URLs    

  6                 Chunking Engine   Create retrieval  Sections → chunks
                                      units             

  7                 Embedding         Generate semantic Text → embeddings
                    Generator         vectors           

  8                 Vector Store      Store/search      Embeddings → results
                                      embeddings        

  9                 Evidence          Select relevant   Query → evidence
                    Retriever         source content    

  10                Gemma 4           Interpret         Evidence → structured
                                      evidence          reasoning

  11                Opportunity       Create            Evidence → JSON
                    Extractor         opportunity       
                                      record            

  12                Eligibility       Apply explicit    Profile + rules →
                    Engine            conditions        status

  13                Reasoning Graph   Represent         Conditions → graph
                                      eligibility logic 

  14                Evidence          Check claims      Claim →
                    Validator         against source    verified/unverified

  15                Contradiction     Identify          Claims → conflicts
                    Detector          conflicting       
                                      information       

  16                Change Detector   Compare           Versions → changes
                                      notification      
                                      versions          

  17                Profile Matcher   Compare user      Profile + opportunity
                                      profile           → match

  18                Confidence Layer  Determine         Evidence + output →
                                      verification      confidence
                                      state             

  19                Action Planner    Generate next     Result + documents →
                                      steps             action plan

  20                Explanation       Simplify verified Evidence →
                    Engine            information       explanation

  21                Streamlit UI      Present results   System output →
                                                        dashboard
  ---------------------------------------------------------------------------

------------------------------------------------------------------------

# 12. Data / Information Flow

``` mermaid
sequenceDiagram
    autonumber

    participant U as User
    participant UI as Streamlit UI
    participant PDF as Document Processor
    participant VDB as FAISS
    participant LLM as Gemma 4
    participant RULE as Eligibility Engine
    participant VERIFY as Verification Layer

    U->>UI: Upload official notification
    UI->>PDF: Process document
    PDF->>PDF: Extract text + page numbers
    PDF->>VDB: Create chunks + embeddings
    VDB-->>UI: Search index ready

    U->>UI: Enter profile
    U->>UI: Ask question

    UI->>VDB: Retrieve relevant evidence
    VDB-->>UI: Top-k chunks + page metadata

    UI->>LLM: Question + evidence
    LLM-->>UI: Structured answer + claims

    UI->>VERIFY: Validate claims against evidence
    VERIFY-->>UI: Verified / uncertain / not found

    UI->>RULE: Profile + extracted eligibility
    RULE-->>UI: Match / mismatch / verification

    UI-->>U: Result + evidence + documents + deadline + action plan
```

### Intermediate representation

Each critical field should retain evidence metadata.

``` json
{
  "field": "income_limit",
  "value": 250000,
  "unit": "INR/year",
  "source_page": 5,
  "evidence": "Relevant extracted notification text",
  "confidence": 0.94,
  "status": "verified_from_source"
}
```

### Evidence chain

``` text
AI Claim
   ↓
Retrieved Source Chunk
   ↓
Page Number
   ↓
Original Notification
```

If the evidence is missing:

``` text
Status = NOT_FOUND / NEEDS_VERIFICATION
```

------------------------------------------------------------------------

# 13. Agentic Workflow

SevaPath is primarily a **RAG pipeline with structured AI modules,
deterministic rules and verification**, rather than a system of many
autonomous agents.

Calling every component an "agent" would add complexity without
improving the solution.

### Bounded retrieval-reasoning loop

``` mermaid
flowchart LR

    A["User Question"] --> B["Retrieve Evidence"]
    B --> C{"Enough Evidence?"}

    C -->|"Yes"| D["Gemma 4"]
    C -->|"No"| E["Refine Search"]
    E --> B

    D --> F{"Critical Claim Verified?"}

    F -->|"Yes"| G["Show Answer + Source"]
    F -->|"No"| H["Needs Verification"]
```

The retrieval refinement loop is bounded.

The system must not repeatedly generate guesses until it finds a
plausible answer.

------------------------------------------------------------------------

# 14. Technology Stack

  -----------------------------------------------------------------------
  Layer                   Technology              Purpose
  ----------------------- ----------------------- -----------------------
  Core AI                 Gemma 4                 Reasoning and
                                                  structured
                                                  interpretation

  Embeddings              BGE-M3 / suitable       Semantic retrieval
                          multilingual model      

  OCR                     Tesseract / suitable    Scanned documents
                          open-source OCR         

  Vector Search           FAISS                   Evidence retrieval

  PDF Processing          PyMuPDF                 Text extraction and
                                                  page metadata

  Backend / Logic         Python                  Orchestration

  Validation              Pydantic                Structured output
                                                  validation

  Storage                 SQLite / JSON           MVP persistence

  UI                      Streamlit               User interface

  Deployment              Docker / local          Reproducible execution
                          environment             
  -----------------------------------------------------------------------

Every technology should have a specific role; unnecessary components
will not be added simply to increase the technology count.

------------------------------------------------------------------------

# 15. Expected Features

## Core MVP

### Document Intelligence

-   Official PDF upload
-   Digital PDF extraction
-   OCR fallback
-   Page tracking
-   Section/chunk processing

### AI Understanding

-   Opportunity extraction
-   Eligibility extraction
-   Deadline extraction
-   Fee extraction
-   Required-document extraction
-   Evidence-grounded question answering
-   Simple-language explanation
-   Hindi/Marathi explanation

### Personalization

-   Basic user profile
-   Eligibility matching
-   Eligibility reasoning graph
-   Condition-by-condition explanation
-   Missing requirement detection

### Trust & Safety

-   Source evidence
-   Page references
-   Confidence/verification state
-   Not-found response
-   Contradiction detection
-   Human verification prompts

### Action

-   Required-document checklist
-   Deadline display
-   Action plan
-   Official application/source link

### Advanced MVP differentiators

-   Notification version comparison
-   Deadline/condition change detection
-   Opportunity match score where sufficient structured data exists

------------------------------------------------------------------------

# 16. Implementation Approach

## Phase 1 --- Foundations

-   Python project structure
-   Streamlit interface
-   PDF upload
-   basic result layout

## Phase 2 --- Document Processing

-   PyMuPDF integration
-   page tracking
-   OCR fallback
-   section detection

## Phase 3 --- Retrieval

-   chunking
-   embeddings
-   FAISS index
-   semantic retrieval

## Phase 4 --- Gemma 4 Integration

-   evidence-first prompting
-   structured output
-   opportunity extraction
-   eligibility interpretation
-   question answering

## Phase 5 --- Eligibility Intelligence

-   rule engine
-   profile matcher
-   reasoning graph
-   three/four-state verification model

## Phase 6 --- Trust Layer

-   evidence validation
-   contradiction detection
-   confidence handling
-   not-found handling

## Phase 7 --- Action Layer

-   document checklist
-   deadline
-   action plan
-   official source link

## Phase 8 --- UI

-   opportunity dashboard
-   eligibility visualization
-   evidence panel
-   reasoning graph
-   language selection

## Phase 9 --- Testing

Test against representative:

-   scholarship notifications
-   recruitment notifications
-   apprenticeships
-   welfare schemes
-   long PDFs
-   scanned documents
-   tables
-   multiple dates
-   exceptions
-   multilingual content

## Phase 10 --- Deployment

-   reproducible environment
-   final integration
-   performance testing
-   documentation
-   public open-source repository

------------------------------------------------------------------------

# 17. Expected Final Output

At the end of the final hackathon, SevaPath should provide a working web
interface.

### Example

``` text
┌────────────────────────────────────────────┐
│ 🇮🇳 SEVAPATH                              │
│ Government Opportunity Intelligence        │
├────────────────────────────────────────────┤
│                                            │
│ 🎓 Government Scholarship                  │
│ Issuer: Example Department                 │
│                                            │
│ Deadline: 15 October 2026                  │
│                                            │
│ YOUR ELIGIBILITY                           │
│ 🟢 LIKELY ELIGIBLE                         │
│                                            │
│ ✓ Age                                      │
│ ✓ Qualification                            │
│ ✓ Category                                 │
│ ✓ State                                    │
│ ⚠ Income certificate verification          │
│                                            │
│ REQUIRED DOCUMENTS                         │
│ ✓ Marksheet                                │
│ ✓ Aadhaar                                  │
│ ⚠ Income Certificate                       │
│                                            │
│ [WHY?] [VIEW EVIDENCE] [ACTION PLAN]      │
│                                            │
│ [OPEN OFFICIAL APPLICATION]                │
└────────────────────────────────────────────┘
```

The evaluator should be able to understand the product without needing
to inspect the implementation.

------------------------------------------------------------------------

# 18. Future Scope / Scalability

## Opportunity Discovery

``` text
Multiple Government Sources
        ↓
SevaPath Knowledge Layer
        ↓
Personalized Opportunity Feed
```

Potential extensions:

-   Multiple government notifications
-   Opportunity search
-   Personalized opportunity ranking
-   Deadline reminders
-   Saved opportunities
-   Notification amendment monitoring
-   Change detection
-   Notification comparison
-   More Indian languages
-   Voice input/output
-   Mobile application
-   Messaging interfaces
-   College/student-cell dashboards
-   Accessibility mode
-   Multilingual retrieval
-   Calendar integration
-   Application preparation guidance

### Long-term vision

``` text
Government Information
        ↓
Verified Knowledge
        ↓
Personalized Opportunities
        ↓
Eligibility Reasoning
        ↓
Clear Action Steps
        ↓
User Application
```

The long-term goal is not to become another unofficial government
portal.

It is to become an **AI interpretation layer between complex public
information and the people who need it**.

------------------------------------------------------------------------

# 19. Open-Source Dependencies / Components

> Exact model and dependency licenses must be re-verified against the
> versions actually used before final release.

  -----------------------------------------------------------------------
  Component               Purpose                 License / Status
  ----------------------- ----------------------- -----------------------
  **Gemma 4 / selected    Core                    Verify exact model
  open-weight model**     government-document     terms
                          reasoning               

  **BGE-M3 / selected     Semantic retrieval      Verify exact model
  embedding model**                               terms

  **FAISS**               Vector search           Open-source

  **PyMuPDF**             PDF extraction          Open-source

  **Tesseract OCR**       OCR fallback            Open-source

  **Streamlit**           Web interface           Open-source

  **Pydantic**            Schema validation       Open-source

  **SQLite**              Local persistence       Public domain

  **Python**              Application runtime     PSF License
  -----------------------------------------------------------------------

Model weights will not be redistributed unless the applicable license
explicitly permits redistribution.

------------------------------------------------------------------------

# 20. Expected Challenges and Mitigation

  -----------------------------------------------------------------------
  Challenge               Why It Happens          Mitigation
  ----------------------- ----------------------- -----------------------
  Long PDFs               Important information   Chunking + retrieval
                          may be distributed      
                          across pages            

  Hallucinated answers    LLM may generate        RAG + evidence
                          unsupported information verification

  Complex eligibility     Multiple conditions and Structured extraction +
                          exceptions              rules + verification

  Scanned PDFs            No machine-readable     OCR fallback
                          text                    

  Tables                  Information may be      Table-aware extraction
                          encoded in layouts      

  Multiple dates          Issue, start, closing   Context-aware date
                          and extension dates can extraction
                          coexist                 

  Amendments              Later notices may       Version/change
                          change earlier          detection
                          information             

  Contradictions          Different clauses may   Contradiction
                          appear inconsistent     detection +
                                                  verification

  Multilingual text       English and Indian      Multilingual
                          languages may be mixed  embeddings + AI
                                                  explanation

  False confidence        AI may sound certain    Confidence +
                          without evidence        verification states

  User profile errors     User may provide        Clearly label profile
                          incorrect information   as user-provided

  Privacy                 Profile data can be     Minimize stored
                          sensitive               personal data

  Broken/missing links    URLs may be absent or   Show only detected
                          invalid                 source links

  Outdated information    Old notifications may   Display source/version
                          no longer apply         dates where available
  -----------------------------------------------------------------------

### Most important safety rule

> **If SevaPath cannot find reliable evidence in the source document, it
> should not manufacture an answer.**

------------------------------------------------------------------------

# 21. Evaluation Strategy

No benchmark results are claimed before implementation and testing.

The final system should be evaluated on representative government
notifications.

## Test Categories

-   Scholarships
-   Recruitment
-   Apprenticeships
-   Welfare schemes

## Document Difficulty

-   Long PDFs
-   Scanned pages
-   Tables
-   Multiple dates
-   Category conditions
-   Income limits
-   Exceptions
-   Multilingual content
-   Amendments where available

## Metrics

  -----------------------------------------------------------------------
  Metric                              Measures
  ----------------------------------- -----------------------------------
  Field Extraction Accuracy           Correctness of dates, age,
                                      qualification, income, fee etc.

  RAG Answer Accuracy                 Whether answers are supported by
                                      source

  Citation/Page Accuracy              Whether cited pages actually
                                      support claims

  Eligibility Accuracy                Correct match/mismatch/verification
                                      result

  Checklist Accuracy                  Required documents captured
                                      correctly

  Not-Found Accuracy                  Correct refusal of unsupported
                                      questions

  OCR Quality                         Extraction quality from scanned
                                      documents

  Multilingual Quality                Preservation of source meaning

  Contradiction Detection             Ability to identify conflicting
                                      conditions

  Change Detection                    Ability to identify changed
                                      information

  End-to-End Latency                  Time from upload to usable result

  Human Correction Rate               Percentage requiring manual
                                      correction
  -----------------------------------------------------------------------

### Baseline comparison

``` text
Baseline:
LLM + full PDF text

vs.

SevaPath:
Chunking
+
Embeddings
+
Retrieval
+
Gemma 4
+
Structured Output
+
Evidence Verification
+
Eligibility Rules
```

The goal is to determine whether retrieval, structure and verification
improve reliability.

------------------------------------------------------------------------

# 22. Responsible AI and Government-Information Safety

  -----------------------------------------------------------------------
  Principle                           Implementation
  ----------------------------------- -----------------------------------
  **Source-first answers**            Important claims should come from
                                      retrieved notification evidence

  **No fabricated facts**             Missing information is returned as
                                      unknown/not found

  **Official-source transparency**    Original notification/application
                                      link is shown when available

  **No eligibility guarantee**        Results are expressed as likely
                                      eligible/not eligible/needs
                                      verification

  **Human verification**              Critical information should be
                                      checked against the official
                                      notification

  **Privacy**                         Store the minimum profile
                                      information required

  **No automatic submission**         MVP does not submit government
                                      applications

  **No document fabrication**         No fake certificates, marksheets or
                                      government documents

  **Uncertainty visibility**          Ambiguous requirements are
                                      explicitly flagged

  **Version awareness**               Notification date/version is shown
                                      where available

  **AI disclosure**                   Users are informed that
                                      explanations are AI-generated
  -----------------------------------------------------------------------

### Important disclaimer

SevaPath is an **information-understanding and assistance tool**.

It does not provide legal advice, government approval or guaranteed
eligibility.

Before submitting an application, users should verify the final
requirements, dates, fees and instructions on the official government
notification or portal.

------------------------------------------------------------------------

# 23. Hackathon Scope

## In Scope --- Final MVP

-   One government notification PDF at a time
-   PDF text extraction
-   OCR fallback
-   RAG-based question answering
-   Gemma 4 reasoning
-   Structured extraction of:
    -   dates
    -   eligibility
    -   qualification
    -   category
    -   income
    -   fees
    -   documents
    -   official links
-   Basic user profile
-   Eligibility matching
-   Eligibility reasoning graph
-   Evidence/page references
-   Deadline display
-   Document checklist
-   Uncertainty handling
-   Simple English explanation
-   Hindi or Marathi explanation
-   Action plan
-   Streamlit-based web interface
-   Small-scale evaluation

## Optional --- Only If Time Permits

-   Multiple notification search
-   Opportunity ranking
-   Saved opportunities
-   Deadline reminders
-   Advanced table extraction
-   Notification comparison
-   Change detection
-   Contradiction detection
-   Voice input

## Out of Scope for the Hackathon

  -----------------------------------------------------------------------
  Feature                             Reason
  ----------------------------------- -----------------------------------
  Automatic government application    Different portals and high risk of
  submission                          incorrect submissions

  Guaranteed eligibility              Final eligibility belongs to the
                                      relevant authority

  Real-time monitoring of every       Too broad for the MVP
  government portal                   

  Training a foundation LLM           Not feasible within hackathon
                                      constraints

  Training a new embedding model      Existing open-source models are
                                      sufficient

  Perfect OCR for every document      Government layouts vary
                                      significantly

  Complete legal interpretation       Outside project scope

  Certificate/document fabrication    Unsafe and inappropriate

  Massive cloud infrastructure        Not necessary for the core
                                      demonstration

  Full native mobile application      Web interface is sufficient for the
                                      final demo
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# Final Architecture Principle

SevaPath follows a simple rule:

``` text
          DON'T JUST ANSWER
                  ↓
          UNDERSTAND THE SOURCE
                  ↓
          RETRIEVE THE EVIDENCE
                  ↓
          REASON OVER THE EVIDENCE
                  ↓
          VERIFY THE IMPORTANT CLAIMS
                  ↓
          MATCH THE USER
                  ↓
          EXPLAIN THE DECISION
                  ↓
          SHOW UNCERTAINTY
                  ↓
          GUIDE THE NEXT ACTION
```

## SevaPath

> **Understand the notification. Verify the evidence. Know your
> eligibility. Take the next step.**

------------------------------------------------------------------------

**🇮🇳 SevaPath --- From Government Information to Verified Action**

*Built for the Hacktober Fest Open Source AI Hackathon.*
:::
