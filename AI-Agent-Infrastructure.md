# 🤖 AI Agent Infrastructure

<p align="center">
  <strong>AI Agents • LLM Orchestration • Local AI • Cloud Infrastructure • Automation</strong>
</p>

<p align="center">
  A hybrid AI infrastructure project combining cloud-based agent orchestration with local language-model inference.
</p>

---

## 📌 Project Status

**Status:** Active Development / Experimentation

**Main Technologies:**

`Python` `Docker` `Linux` `Ollama` `LLM APIs` `REST APIs` `Tailscale` `SSH` `Oracle Cloud`

---

## 🚀 Project Overview

**AI Agent Infrastructure** is an experimental infrastructure project focused on understanding how autonomous AI agents can operate as persistent software services rather than only as conversational interfaces.

The project combines:

* AI agent orchestration
* Large Language Models
* Local AI inference
* Cloud infrastructure
* Containerized services
* Private networking
* API-based communication
* Tool execution
* Messaging integrations
* Automation

One of the main objectives was to separate the **AI agent runtime** from the **machine responsible for model inference**.

This resulted in a hybrid architecture where an agent can run continuously on a cloud VPS while communicating securely with an AI model running on local hardware.

---

## 🎯 Project Motivation

A basic LLM application usually follows a simple workflow:

```text
User
  ↓
Language Model
  ↓
Response
```

This project explores a more complete architecture:

```text
User
  ↓
AI Agent
  ↓
Reasoning / Decision
  ↓
Tools and APIs
  ↓
External Systems
  ↓
Result
  ↓
AI Agent
  ↓
Response
```

The goal is to explore the engineering required to transform a language model into a component of a broader software system.

---

## 🏛️ Hybrid Architecture

One of the most important experiments in this project was separating agent orchestration from model inference.

The architecture uses two different environments:

### Cloud Environment

A Linux VPS runs the AI agent infrastructure.

Its responsibilities include:

* Running the agent service
* Receiving messages
* Coordinating model requests
* Managing integrations
* Executing automated workflows
* Remaining available independently from the development machine

### Local Environment

A local computer runs the language model using Ollama.

Its responsibilities include:

* Model inference
* GPU acceleration
* Providing an OpenAI-compatible API endpoint

The result is a hybrid system:

```text
┌───────────────────────────────┐
│          Cloud VPS            │
│                               │
│       AI Agent Runtime        │
│       Docker Container        │
│       External Services       │
│       Automation              │
└───────────────┬───────────────┘
                │
                │ Private Network
                │
                ▼
┌───────────────────────────────┐
│        Local Computer         │
│                               │
│           Ollama              │
│        Local LLM Model        │
│        GPU Inference          │
└───────────────────────────────┘
```

---

## 🤖 Agent Orchestration

The project has used **Hermes Agent** as an orchestration layer.

Hermes is responsible for communicating with the configured language-model endpoint while providing the infrastructure required for agent-oriented workflows.

The basic architecture is:

```text
Hermes Agent
     ↓
OpenAI-Compatible API
     ↓
Ollama
     ↓
Local Language Model
```

This separation allows the agent runtime to communicate with different model providers without requiring the entire system architecture to be redesigned.

---

## 🐳 Containerized Deployment

The agent environment runs inside **Docker** on a Linux VPS.

Containerization provides several advantages:

* Dependency isolation
* Reproducible environments
* Easier deployment
* Simplified service management
* Cleaner configuration
* Easier recovery and restart

The agent therefore operates independently from the host operating system configuration.

---

## ☁️ Cloud Infrastructure

The orchestration environment has been deployed on an **Oracle Cloud VPS running Linux**.

The cloud server acts as the persistent infrastructure layer.

Conceptually:

```text
Internet
   ↓
Cloud VPS
   ↓
Docker
   ↓
AI Agent
```

This allows the agent service itself to remain available without requiring the local development environment to host the entire application.

---

## 🧠 Local AI Inference

The inference layer uses **Ollama** to run language models locally.

One of the models used during development was:

```text
qwen2.5:7b
```

Ollama exposes an HTTP interface that can also be accessed through an OpenAI-compatible API format.

This makes it possible for software designed around common LLM APIs to communicate with locally hosted models.

---

## 🔌 OpenAI-Compatible API

A major architectural decision was using an **OpenAI-compatible interface** between the agent runtime and model provider.

Instead of tightly coupling the agent to a specific model:

```text
Agent
  ↓
Specific Model
```

the architecture becomes:

```text
Agent
  ↓
Standard API Interface
  ↓
Model Provider
```

This makes it easier to experiment with different inference providers.

For example:

```text
                  AI Agent
                     │
                     ▼
           OpenAI-Compatible API
                     │
          ┌──────────┼──────────┐
          │          │          │
          ▼          ▼          ▼
       Ollama      Remote     Alternative
       Local       Provider      LLM
```

---

## 🔒 Private Networking

One of the main infrastructure concerns was avoiding direct public exposure of the local Ollama server.

Instead of exposing the inference endpoint openly to the internet, the project uses private networking techniques.

The main solution explored was **Tailscale**.

```text
Cloud VPS
   │
   ▼
Tailscale Private Network
   │
   ▼
Local Computer
   │
   ▼
Ollama API
```

This allows the VPS and local computer to communicate as if they were part of the same private network.

---

## 🛡️ Avoiding Public Model Exposure

The intended network design avoids an architecture such as:

```text
Internet
   ↓
Public Ollama Port
   ↓
Local Model
```

and instead favors:

```text
Cloud VPS
   ↓
Private Network
   ↓
Local Ollama
```

This reduces unnecessary public exposure of the local inference service.

---

## 🔐 SSH Tunneling

SSH tunneling has also been used during the infrastructure experiments.

An SSH tunnel can create a secure connection between remote and local services without requiring the application endpoint itself to be publicly exposed.

Conceptually:

```text
Application
   ↓
localhost
   ↓
SSH Tunnel
   ↓
Remote Service
```

This provided practical experience with secure service-to-service communication.

---

## 📡 Telegram Integration

The agent infrastructure has also been connected to **Telegram**.

Telegram acts as an external interface through which a user can interact with the AI agent.

The flow can be represented as:

```text
User
   ↓
Telegram
   ↓
Cloud Agent
   ↓
Model API
   ↓
LLM
   ↓
Agent
   ↓
Telegram Response
```

This allows the AI agent to operate through a messaging interface rather than depending on a locally running desktop application.

---

## 🧰 Tool-Oriented Agents

The broader objective of the project is not limited to text generation.

The infrastructure is intended to support agents capable of interacting with external tools and services.

The general pattern is:

```text
User Request
     ↓
AI Agent
     ↓
Model Decision
     ↓
Tool Call
     ↓
External System
     ↓
Tool Result
     ↓
AI Agent
     ↓
Final Response
```

Possible tool categories include:

* REST APIs
* Messaging systems
* Data processing tools
* External services
* Scheduled operations
* Automation workflows

---

## ⚙️ Automation

Another important area of experimentation is autonomous or scheduled execution.

Instead of requiring a human message before every action, an agent infrastructure can support tasks triggered by:

* Schedules
* External events
* API requests
* Messages
* System conditions

Conceptually:

```text
Trigger
   ↓
Agent
   ↓
Model / Logic
   ↓
Tool
   ↓
Action
```

This moves the system closer to an autonomous software-service architecture.

---

## 🧩 Infrastructure Components

| Layer                     | Technology                   |
| ------------------------- | ---------------------------- |
| **Agent Runtime**         | Hermes Agent                 |
| **Local Model Runtime**   | Ollama                       |
| **Local Model Used**      | Qwen2.5 7B                   |
| **Containerization**      | Docker                       |
| **Operating System**      | Linux                        |
| **Cloud Infrastructure**  | Oracle Cloud VPS             |
| **Private Networking**    | Tailscale                    |
| **Remote Administration** | SSH                          |
| **API Communication**     | REST / OpenAI-Compatible API |
| **Messaging Interface**   | Telegram                     |

---

## 🏗️ Complete Architecture

```text
                         User
                           │
                           ▼
                       Telegram
                           │
                           ▼
              ┌─────────────────────────┐
              │       Cloud VPS         │
              │                         │
              │      Linux Server       │
              │           │             │
              │         Docker          │
              │           │             │
              │     Hermes Agent        │
              └───────────┬─────────────┘
                          │
                          │ OpenAI-Compatible API
                          │
                          ▼
                 Tailscale Network
                          │
                          ▼
              ┌─────────────────────────┐
              │      Local Computer     │
              │                         │
              │          Ollama         │
              │             │           │
              │             ▼           │
              │       Local LLM         │
              │       GPU Inference     │
              └─────────────────────────┘
```

---

## 🧠 Separation of Responsibilities

An important architectural lesson from the project is that an AI system can be divided into multiple independent layers.

### Agent Layer

Responsible for:

* Conversation flow
* Tool selection
* Workflow coordination
* External integrations

### Model Layer

Responsible for:

* Language understanding
* Generation
* Reasoning support
* Tool-call decisions

### Infrastructure Layer

Responsible for:

* Running services
* Networking
* Availability
* Containers
* Remote communication

### Integration Layer

Responsible for:

* Messaging
* APIs
* External tools
* Automation triggers

The resulting structure can be summarized as:

```text
Interface
   ↓
Agent
   ↓
Model
   ↓
Tools
   ↓
Infrastructure
```

---

## 🧪 Experimental Nature

This project is intentionally an experimentation environment.

It has been used to explore questions such as:

* Can an agent run in the cloud while inference happens locally?
* How can local models be accessed securely from remote infrastructure?
* How can different LLM providers use the same agent architecture?
* How can messaging systems become interfaces for autonomous agents?
* How should agent, model and infrastructure responsibilities be separated?

The project evolves as new models, tools and orchestration technologies are tested.

---

## 🚧 Technical Challenges

### 1. Remote Model Connectivity

The agent and model run on different machines.

The system therefore required a reliable way for the VPS to reach the local inference API without unnecessary public exposure.

**Approach:** private networking through Tailscale and experimentation with SSH tunneling.

---

### 2. Provider Compatibility

Agent software often expects APIs compatible with specific providers.

Using an OpenAI-compatible interface made it possible to connect the orchestration layer with Ollama while keeping the integration relatively provider-independent.

---

### 3. Persistent Agent Availability

Running the orchestration layer on a VPS introduces infrastructure requirements such as:

* Container lifecycle
* Configuration persistence
* Network connectivity
* Service availability

Docker and Linux service infrastructure provided a practical environment for experimenting with these concerns.

---

### 4. Local vs. Cloud Resources

Running every component in the cloud can increase infrastructure requirements.

Running everything locally reduces availability.

The hybrid architecture explores a compromise:

```text
Cloud
  ↓
Availability and orchestration

Local Hardware
  ↓
GPU inference
```

---

## 📚 Key Learnings

The project reinforced that building an AI application involves significantly more than selecting a language model.

A larger AI system may require:

```text
Language Model
      +
Agent Runtime
      +
Tool Integration
      +
API Layer
      +
Networking
      +
Cloud Infrastructure
      +
Security
      +
Automation
```

Another important lesson was that model inference and agent orchestration do not need to happen on the same machine.

By separating them, the architecture becomes more flexible and allows local compute resources to be combined with persistent cloud services.

---

## 🔬 Current Direction

The project continues to explore:

* AI agent orchestration
* Local language models
* Alternative LLM providers
* Tool calling
* API integrations
* Persistent agents
* Automation
* Hybrid cloud/local architectures
* Secure remote inference
* Messaging interfaces

Future experiments may expand the number of tools and external systems available to the agent.

---

## 🎓 Relevance to My Technical Development

This project represents the intersection of several areas I am currently exploring:

```text
Artificial Intelligence
          +
Backend Engineering
          +
Cloud Infrastructure
          +
Networking
          +
Automation
```

It has provided practical experience not only with AI models, but with the infrastructure required to make AI systems operate as distributed software services.

---

## 📌 Project Summary

**AI Agent Infrastructure** explores a hybrid architecture where an AI agent operates in cloud infrastructure while communicating securely with local model inference.

The architecture can be summarized as:

```text
User
  ↓
Messaging / API
  ↓
Cloud AI Agent
  ↓
Private Network
  ↓
Local LLM
  ↓
Tools and External Services
```

The project demonstrates practical experimentation with:

* AI Agents
* LLM orchestration
* Local inference
* REST APIs
* Linux
* Docker
* Cloud VPS infrastructure
* Private networking
* SSH
* Telegram integration
* Distributed AI architecture

---

<p align="center">
  <i>Exploring how language models can become components of real, distributed software infrastructure.</i>
</p>
