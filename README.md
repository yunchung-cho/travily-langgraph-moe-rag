# Travily: Stateful MoE Agent Ecosystem with RAG & Semantic Backtracking

An advanced, production-grade AI Agent framework that orchestrates multi-agent collaboration, real-time factual grounding, and self-correcting reasoning loops. Built entirely on top of **LangGraph** and powered by the latest **Google Gemini (3.x Gen)** models, Travily implements a stateful, cyclic Mixture of Experts (MoE) architecture capable of resolving complex, high-ambiguity, and time-sensitive queries.

---

## 🏗️ Repository Architecture

This repository is structured to demonstrate the evolutionary progression of agentic workflows—moving from isolated parametric knowledge to a fully grounded, self-correcting hybrid intelligence ecosystem.

```text
.
├── README.md                          # Comprehensive project documentation
├── 01_base_moe_backtracking/
│   └── Gemini_LangGraph_MoE.ipynb    # Base architecture (Parametric MoE + Backtracking)
└── 02_rag_enhanced_moe/
    └── Travily_RAG_MoE_Agent.ipynb    # Production-tier (Web RAG + Cross-Auditing MoE)
```

---

## 💡 Core Engineering Concepts

### 1. Mixture of Experts (MoE) Orchestration
Instead of channeling a query through a single monolithic LLM, Travily routes tasks to diverse agent profiles configured with distinct cognitive biases:
*   **Expert A (gemini-3.5-flash-lite | Temp 0.7):** Tailored for creative synthesis, rapid brainstorming, and expansive exploration.
*   **Expert B (gemini-3.6-flash | Temp 0.4):** Tailored for rigid analytical deduction, deterministic reasoning, and structural validation.

### 2. Semantic Backtracking & Pruning
Traditional sequential LLM chains suffer from cascading errors—if an agent makes a mistake early on, the entire pipeline fails. Travily solves this by introducing a **Feedback Loop mapped to a Depth-First Search (DFS) with Pruning**:
*   Outputs are strictly audited by a deterministic **Evaluator Node**.
*   Upon detecting an misalignment or factual gap, the graph triggers a semantic prune, aborting the forward execution.
*   The system state rolls back (**Backtracks**) to the generation node, injecting the auditor's precise feedback to guide self-correction.

### 3. RAG-Driven Triangulation
In the RAG-enhanced variant, the system eliminates hallucinations by anchoring the entire debate process in real-time truth. A dedicated **Retrieval Node (powered by Tavily API)** injects fresh web knowledge directly into the graph state. The Evaluator then performs cross-verification, checking not only if the experts agree with each other, but if they are rigorously bounded by the retrieved facts.

---

## 📊 Evolutionary Comparison

| Feature | Phase 1: Base MoE (`01_base_moe_backtracking`) | Phase 2: RAG-Enhanced (`02_rag_enhanced_moe`) |
| :--- | :--- | :--- |
| **Knowledge Base** | Internal Parametric Knowledge (Static) | Real-time Web Context Integration (Dynamic) |
| **Orchestration** | Stateful LangGraph Loop | Stateful LangGraph Loop |
| **Expert Profiles** | Divergent Temperature Scaling | Divergent Temperature Scaling + Model Tiering |
| **Auditing Gate** | Cross-Expert Agreement | Three-Way Factual Grounding (Context ↔ A ↔ B) |
| **Backtracking Behavior** | Re-generation based on logical debate | Re-generation focused on closing factual gaps |
| **Best Used For** | Logic puzzles, conceptual trade-off analysis | Fresh trend analysis, market research, factuality checks |

---

## 🚀 Getting Started

### Prerequisites

Ensure you have your API credentials ready. You will need:
1.  **Google Gemini API Key** (Accessible via Google AI Studio)
2.  **Tavily API Key** (For the RAG-enhanced model)

If you are running these notebooks in Google Colab, securely store your keys inside the **Secrets** manager (`🔑` tab on the left sidebar) under the names `GeminiAPI` and `TAVILY_API_KEY`.

### Installation

Install the required core dependencies directly inside your notebook environment:

```bash
pip install langchain-core langchain-google-genai langchain-community tavily-python langgraph
```

---

## 🛠️ Workflow Mechanics

1.  **Ingestion & Retrieval:** The query is intercepted; for the RAG pipeline, fresh contextual text chunks are saved into the `State`.
2.  **Parallel Generation:** Experts A and B pull from the synchronized state and independently generate analytical drafts.
3.  **The Factual Audit:** The Evaluator compiles the context and expert inputs, returning a structured JSON payload (`is_consistent`, `feedback`).
4.  **The Routing Decision:**
    *   If `is_consistent` is `True`, the graph flows cleanly to the **Final Judge Node** to produce a unified master briefing.
    *   If `is_consistent` is `False`, the graph forces an internal rollback, executing a **Backtrack** to adjust the path up to a predefined retry threshold.
