# RAG with Knowledge Graphs using Neo4j

A Retrieval-Augmented Generation (RAG) system that combines the power of Knowledge Graphs with Large Language Models to provide accurate, context-aware responses.

## 🌟 Features

- **Knowledge Graph Construction**: Automatically builds a knowledge graph from text documents
- **Hybrid Retrieval**: Combines vector similarity search with graph traversal for enhanced context
- **Entity Extraction**: Automatically identifies and extracts entities and their relationships
- **Conversational AI**: Maintains conversation context for follow-up questions
- **Visualization**: Interactive graph visualization using yFiles

## 🏗️ Architecture

```
User Query
    ↓
Entity Extraction (LLM)
    ↓
┌─────────────────┴──────────────────┐
│                                    │
Structured Retrieval          Vector Search
(Graph Traversal)            (Embeddings)
│                                    │
└─────────────────┬──────────────────┘
                  ↓
          Context Combination
                  ↓
          LLM Answer Generation
                  ↓
            Final Response
```

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Neo4j Database (AuraDB or local instance)
- Groq API Key (for Llama 3.3 70B)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/yourusername/rag-knowledge-graph-neo4j.git
cd rag-knowledge-graph-neo4j
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Create a `config.py` file with your credentials:
```python
GROQ_API_KEY = "your-groq-api-key"
NEO4J_URI = "neo4j+s://your-instance.databases.neo4j.io"
NEO4J_USERNAME = "neo4j"
NEO4J_PASSWORD = "your-password"
```

### Usage

Open and run the Jupyter notebook:
```bash
jupyter notebook RAG_Knowledge_Graph_Neo4j.ipynb
```

## 📖 Example Queries

```python
# Simple query
Q: "Which house did Elizabeth I belong to?"
A: "Elizabeth I belonged to the House of Tudor."

# Follow-up query (uses conversation context)
Q: "When was she born?"
A: "Elizabeth I was born on 7 September 1533."

# Complex relationship query
Q: "Who were Elizabeth I's parents and siblings?"
A: "Elizabeth I's parents were Henry VIII and Anne Boleyn. 
    Her siblings included Edward VI and Mary I."
```

## 🔧 Configuration

### Neo4j Setup

1. Create a free Neo4j AuraDB instance at [neo4j.com/cloud/aura](https://neo4j.com/cloud/aura/)
2. Note your connection URI, username, and password
3. Add these credentials to your `config.py` file

## 🎯 Key Components

### 1. Document Processing
- Loads data from Wikipedia (or custom sources)
- Splits documents into manageable chunks
- Maintains context with overlapping windows

### 2. Knowledge Graph Construction
- Extracts entities and relationships using LLM
- Builds structured graph representation in Neo4j
- Creates bidirectional relationships

### 3. Hybrid Retrieval System
- **Vector Search**: Finds semantically similar content using embeddings
- **Graph Traversal**: Explores entity relationships and connections
- **Combined Results**: Merges both approaches for comprehensive context

### 4. Conversational Interface
- Maintains chat history
- Rephrases follow-up questions with context
- Generates accurate, concise responses

## 📊 Graph Structure

The system creates the following node types:
- **Document**: Original text chunks with embeddings
- **Entity**: Extracted persons, organizations, locations
- **Relationships**: Custom relationships between entities

Example relationships:
```cypher
(Elizabeth I)-[:CHILD_OF]->(Henry VIII)
(Elizabeth I)-[:MEMBER_OF]->(House of Tudor)
(Elizabeth I)-[:QUEEN_OF]->(England)
```

## 🔬 Advanced Features

### Custom Entity Extraction
Modify the entity schema to extract domain-specific entities:
```python
class CustomEntities(BaseModel):
    persons: List[str]
    organizations: List[str]
    locations: List[str]
    dates: List[str]
```

### Custom Relationships
Add domain-specific relationship types in the graph transformer.

### Performance Optimization
- Use caching for frequently asked questions
- Implement query result pagination
- Optimize vector index parameters

## 🛠️ Tech Stack

- **LLM**: Groq (Llama 3.3 70B)
- **Graph Database**: Neo4j
- **Orchestration**: LangChain
- **Embeddings**: HuggingFace (sentence-transformers)
- **Visualization**: yFiles Jupyter Graphs


⭐ Star this repo if you find it helpful!
