# Multi-Agent & MoE Enhanced RAG Project

This repository focuses on the research and implementation of advanced LLM architectures, specifically featuring a Multi-Agent-based document analysis system (DocChat), Mixture of Experts (MoE) backtracking mechanisms, and RAG-enhanced MoE models.

## 📁 Repository Structure

The project is organized into three core modules based on their unique architectural characteristics:

* **`00_Multi_Agent_RAG`**
  * An implementation of a document-based conversational system (DocChat) using a Multi-Agent framework.
  * Facilitates collaboration among multiple specialized agents to search, analyze, and synthesize insights from dense, complex document repositories.
* **`01_base_moe_backtracking`**
  * Research and codebase for integrating backtracking algorithms into Mixture of Experts (MoE) architectures to optimize token routing.
  * Focuses on detecting routing inefficiencies and reverting to alternative branch nodes to evaluate optimal paths.
* **`02_rag_enhanced_moe`**
  * A hybrid architecture that maximizes model throughput and contextual accuracy by coupling Retrieval-Augmented Generation (RAG) with MoE.
  * Designed so that external knowledge base retrievals directly inform both the MoE expert routing gate and the final token generation.

