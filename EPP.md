# ⚙️ Exercise Processing Pipeline — EPP

<p align="center">
  <strong>Data Processing • Software Architecture • Validation • Reliability • Educational Technology</strong>
</p>

<p align="center">
  A modular pipeline designed to transform raw educational exercises into structured, validated and reusable learning content.
</p>

---

## 📌 Project Status

**Status:** Validation and Stabilization Phase

**Main Technologies:**

`Python` `Data Processing` `Event-Driven Architecture` `Automation` `LLMs` `Testing`

---

## 🚀 Project Overview

The **Exercise Processing Pipeline (EPP)** is a modular content-processing architecture designed to collect, clean, structure and validate educational exercises from heterogeneous sources.

The project evolved from an earlier scraper-oriented approach.

Instead of creating a single component responsible for downloading, cleaning, interpreting and validating content, EPP separates the workflow into specialized processing stages.

The main architecture is:

```text
Downloader
    ↓
Cleaner
    ↓
Parser
    ↓
Validator
    ↓
Knowledge Builder
```

Each component has a clearly defined responsibility.

This makes the system easier to test, maintain, monitor and evolve.

---

## 🎯 Problem

Educational exercises available online rarely follow the same structure.

Different sources may contain:

* Different HTML structures
* Navigation elements
* Advertisements
* Repeated content
* Missing information
* Incorrect formatting
* Inconsistent answer structures
* Unexpected characters
* Broken alternatives
* Different question layouts

A traditional scraper can quickly become difficult to maintain when all these responsibilities are handled inside a single extraction function.

A simplified monolithic design may look like:

```text
Download
    ↓
Clean
    ↓
Parse
    ↓
Validate
    ↓
Transform
    ↓
Save
```

When all these responsibilities exist inside the same component, a failure in one stage can affect the entire process.

EPP was designed to avoid this problem.

---

## 🏛️ Architecture

The architecture is based on specialized processing stages.

```text
Raw Source
    ↓
Downloader
    ↓
Raw Content
    ↓
Cleaner
    ↓
Clean Content
    ↓
Parser
    ↓
Structured Exercise
    ↓
Validator
    ↓
Validated Exercise
    ↓
Knowledge Builder
    ↓
Reusable Educational Content
```

Each stage receives input from the previous stage and produces output for the next one.

---

## 📥 Downloader

The **Downloader** is responsible for obtaining raw content from external sources.

Its responsibility is acquisition, not interpretation.

Typical responsibilities include:

* Sending HTTP requests
* Retrieving source content
* Handling connection failures
* Handling timeouts
* Detecting incomplete downloads
* Passing the retrieved content to the next stage

Conceptually:

```text
URL
 ↓
Downloader
 ↓
Raw Source Content
```

The Downloader should not need to understand the educational structure of the content.

---

## 🧹 Cleaner

The **Cleaner** receives raw content and removes information that is irrelevant to exercise extraction.

Examples may include:

* Navigation menus
* Advertisements
* Footer elements
* Repeated layout components
* Unnecessary HTML
* Decorative content
* Unrelated text

The objective is to reduce noise before structural interpretation begins.

```text
Raw Web Content
       ↓
     Cleaner
       ↓
Relevant Content
```

Keeping cleaning separate from parsing helps prevent source-specific layout problems from affecting the entire architecture.

---

## 🧩 Parser

The **Parser** converts cleaned content into structured educational information.

Its responsibility is to identify the logical components of an exercise.

For example:

```text
Clean Content
      ↓
    Parser
      ↓
Question
Alternatives
Answer
Explanation
Metadata
```

The parser focuses on structure.

It does not automatically assume that the extracted exercise is valid.

Validation is handled by the next stage.

---

## ✅ Validator

The **Validator** checks whether parsed exercises meet the expected structural and content requirements.

Possible validation checks include:

* Question text exists
* Required fields are present
* Alternatives exist when required
* Answer format is valid
* Data types are correct
* Exercise structure is consistent
* Required metadata exists

The validator may classify exercises as:

```text
Parsed Exercise
      ↓
   Validator
    /      \
   /        \
Valid      Invalid
  │           │
  ▼           ▼
Continue   Reject / Flag
```

Invalid content should not silently enter the final educational dataset.

---

## 🧠 Knowledge Builder

The **Knowledge Builder** receives validated exercises and prepares them for use by downstream educational systems.

Its objective is to transform validated data into reusable learning structures.

Possible outputs may include:

* Structured question banks
* Markdown content
* Educational datasets
* Study materials
* Content consumed by CourseForge

Conceptually:

```text
Validated Exercise
       ↓
Knowledge Builder
       ↓
Educational Knowledge
```

This separates extraction from presentation.

---

## 🔄 Modular Processing

A central design principle of EPP is avoiding a single large function responsible for every processing step.

Instead of:

```text
download_clean_parse_validate_build()
```

the architecture favors independent components:

```text
Downloader
Cleaner
Parser
Validator
Knowledge Builder
```

This improves:

* Testability
* Maintainability
* Failure isolation
* Reprocessing
* Observability
* Component replacement

---

## 🧱 Separation of Concerns

Each component should focus on one primary responsibility.

```text
Downloader
    ↓
Gets content

Cleaner
    ↓
Removes noise

Parser
    ↓
Creates structure

Validator
    ↓
Checks correctness

Knowledge Builder
    ↓
Creates reusable output
```

This makes it easier to identify where a failure happened.

For example, if a website changes its HTML layout, the issue may affect the Cleaner or Parser without requiring a complete redesign of the pipeline.

---

## 🔁 Event-Oriented Architecture

The architecture was designed around an event-oriented processing model.

Instead of components depending directly on each other's internal implementation, each stage can conceptually react to the output of another stage.

```text
Event
 ↓
Processing Component
 ↓
Result
 ↓
Next Event
```

A simplified flow may look like:

```text
ContentDownloaded
        ↓
Cleaner
        ↓
ContentCleaned
        ↓
Parser
        ↓
ExerciseParsed
        ↓
Validator
        ↓
ExerciseValidated
```

This reduces coupling between components.

---

## 💥 Failure Isolation

A major objective of the architecture is preventing one malformed item from stopping the entire processing workflow.

For example:

```text
Exercise A → Valid
Exercise B → Valid
Exercise C → Invalid
Exercise D → Valid
Exercise E → Valid
```

Instead of:

```text
Exercise C fails
       ↓
Entire pipeline stops
```

the intended behavior is closer to:

```text
Exercise C fails
       ↓
Failure detected
       ↓
Item isolated
       ↓
Pipeline continues
```

This is especially important when processing large educational datasets.

---

## 🧪 Validation Strategy

A major phase of the project focuses on validating the reliability of the pipeline.

The validation plan is divided into multiple stages.

---

## Phase 1 — Diversity Testing

The first objective is testing whether the system works with structurally different sources.

The plan includes testing approximately:

```text
10 different websites or source structures
```

The goal is to prevent the architecture from becoming unintentionally optimized for only one type of page.

The system should be exposed to different:

* HTML layouts
* Question formats
* Answer structures
* Content organization
* Source behavior

---

## Phase 2 — Volume Testing

After basic diversity testing, the next stage evaluates larger processing workloads.

One important milestone is:

```text
1,000 exercises
```

The objective is to identify problems that may not appear during small manual tests.

These may include:

* Memory accumulation
* Slow processing
* Queue growth
* Repeated errors
* Unexpected performance degradation

---

## Phase 3 — Chaos Testing

The pipeline is also tested under intentionally introduced failure conditions.

The validation plan includes several failure scenarios.

Examples include:

* Network failures
* Connection timeouts
* Invalid HTML
* Missing fields
* Unexpected source structure
* Corrupted content
* Invalid AI output
* Parsing failures
* Dependency failures
* Incomplete responses

The goal is not only to verify:

```text
Does the pipeline work?
```

but also:

```text
How does the pipeline fail?
```

---

## 🧨 Chaos Engineering Mindset

A reliable processing system must consider abnormal situations.

Normal execution:

```text
Valid Input
    ↓
Pipeline
    ↓
Valid Output
```

Failure-oriented execution:

```text
Invalid Input
     ↓
Detection
     ↓
Isolation
     ↓
Logging
     ↓
Recovery
```

Understanding failure behavior is an important part of the project.

---

## Phase 4 — Stress Testing

The validation plan also includes progressively larger workloads.

Example progression:

```text
50 exercises
     ↓
100 exercises
     ↓
500 exercises
     ↓
1,000 exercises
     ↓
5,000 exercises
     ↓
10,000 exercises
```

The objective is to observe how the pipeline behaves as workload increases.

---

## 📊 Stress Test Metrics

Important metrics include:

* Processing time
* CPU usage
* Memory usage
* Throughput
* Backlog size
* Failure rate

These measurements help identify where the architecture begins to degrade.

---

## Phase 5 — Regression Testing

Another important part of the validation strategy is regression testing.

The project uses the concept of **Golden Datasets**.

A Golden Dataset contains known inputs and their expected outputs.

```text
Known Input
    ↓
Current Pipeline
    ↓
Generated Output
    ↓
Comparison
    ↓
Expected Output
```

If a future change modifies previously correct behavior, regression tests can detect the problem.

---

## 🥇 Golden Dataset Concept

The workflow can be represented as:

```text
Version A
   ↓
Validated Output
   ↓
Golden Dataset
   ↓
Version B
   ↓
New Output
   ↓
Compare
```

This is especially important when improving parsers and validators because changes that fix one source may accidentally break another.

---

## Phase 6 — Final Validation Report

The final stage consolidates the validation process into a structured report.

The report can summarize:

* Tested sources
* Processing volumes
* Failure scenarios
* Stress test results
* Regression results
* Performance metrics
* Remaining limitations

The objective is to provide evidence about the stability of the system rather than relying only on manual observation.

---

## 🔒 Architecture Freeze

During the validation phase, the project follows an architecture freeze.

The principle is:

```text
Stop adding features
        ↓
Test existing architecture
        ↓
Measure behavior
        ↓
Identify failures
        ↓
Fix reliability problems
        ↓
Validate again
```

The objective is to prevent constant feature development from hiding structural problems.

---

## 🤖 AI-Assisted Processing

Some parts of the broader content-processing workflow may use language models.

AI can assist with tasks such as:

* Content interpretation
* Structure normalization
* Explanation generation
* Knowledge transformation

However, AI output is not treated as automatically correct.

Possible failure scenarios include:

* Missing fields
* Invalid JSON or structure
* Unexpected formatting
* Hallucinated information
* Provider timeouts
* Incomplete responses

Because of this, AI-generated output should still pass through validation.

```text
LLM Output
    ↓
Validator
   /    \
Valid   Invalid
```

This treats AI as a component of the pipeline rather than as an unquestioned source of truth.

---

## 🔗 CourseForge Integration

One of the main intended downstream systems for EPP is **CourseForge**.

The responsibilities remain separate.

```text
External Sources
       ↓
      EPP
       ↓
Structured and Validated Exercises
       ↓
  CourseForge
       ↓
Educational Material
       ↓
    Students
```

EPP focuses on processing and validation.

CourseForge focuses on organization and presentation.

This separation allows both systems to evolve independently.

---

## 🏗️ Conceptual System Architecture

```text
┌──────────────────────────────┐
│       External Sources       │
│                              │
│ Websites                     │
│ Educational Resources        │
│ Exercise Collections         │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│          Downloader          │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│           Cleaner            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│            Parser            │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│          Validator           │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      Knowledge Builder       │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│      Educational Systems     │
│                              │
│ CourseForge                  │
│ Question Banks               │
│ Study Materials              │
└──────────────────────────────┘
```

---

## 🧠 Engineering Concepts Demonstrated

The project explores practical concepts including:

* Data pipeline architecture
* Event-oriented systems
* Separation of concerns
* Data validation
* Failure isolation
* Error recovery
* Stress testing
* Chaos testing
* Regression testing
* Golden datasets
* Performance measurement
* AI output validation
* Educational data processing

---

## 🚧 Main Technical Challenges

### 1. Heterogeneous Sources

Different websites represent exercises using different structures.

The architecture therefore needs to handle variation without becoming completely source-specific.

---

### 2. Invalid Content

Not every retrieved exercise is complete or usable.

The system must detect invalid content before it reaches downstream educational systems.

---

### 3. Failure Recovery

Network failures and parsing errors should not automatically stop the entire processing process.

The pipeline therefore needs to isolate errors and allow safe continuation.

---

### 4. AI Reliability

If language models are used during processing, their output must be treated as potentially invalid.

This requires additional validation.

---

### 5. Performance at Scale

A workflow that performs well with ten exercises may behave very differently with thousands.

Stress testing is therefore part of the architecture validation process.

---

## 📚 Key Learnings

One of the main lessons behind EPP is that **scraping and educational content processing are different responsibilities**.

A monolithic scraper may gradually accumulate responsibilities such as:

```text
Networking
    +
HTML Cleaning
    +
Parsing
    +
Validation
    +
AI Processing
    +
Persistence
    +
Recovery
```

When all of these responsibilities exist in the same component, the architecture becomes increasingly difficult to maintain.

EPP instead emphasizes:

```text
Small Components
      +
Clear Responsibilities
      +
Validation
      +
Failure Isolation
```

Another important lesson was that successful execution alone is not enough to demonstrate system reliability.

A reliable system also needs to be tested under:

* Bad input
* High volume
* Network failures
* Dependency failures
* Unexpected outputs

---

## 🔬 Current Development Phase

The project is currently focused on **stabilization and validation**.

The priority is not adding large amounts of new functionality.

Current goals include:

* Testing different source structures
* Increasing processing volume
* Simulating failures
* Measuring system behavior
* Detecting regressions
* Improving reliability
* Preparing downstream integration

---

## 🎓 Educational Technology Context

EPP exists within a broader educational technology workflow.

Its purpose is not merely extracting web content.

The goal is transforming unstructured educational material into reliable structured data that can later support:

* Courses
* Question banks
* Study material
* Educational websites
* Automated learning workflows

Conceptually:

```text
Unstructured Educational Content
              ↓
             EPP
              ↓
Structured Educational Knowledge
              ↓
Learning Systems
```

---

## 📌 Project Summary

The **Exercise Processing Pipeline** represents the evolution from a scraper-centered solution toward a modular processing architecture.

The main transformation can be summarized as:

```text
Monolithic Scraper
        ↓
Modular Processing Pipeline
        ↓
Validation and Failure Isolation
        ↓
Reliable Educational Data
```

From an engineering perspective, EPP demonstrates practical exploration of:

* Software architecture
* Data pipelines
* Reliability engineering
* Testing strategies
* Validation
* Failure handling
* Performance analysis

From an educational perspective, the project provides infrastructure for transforming raw exercise sources into structured learning resources.

---

<p align="center">
  <i>A system is not truly reliable only because it works under ideal conditions — it must also behave predictably when things go wrong.</i>
</p>
