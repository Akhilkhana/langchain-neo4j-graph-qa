# LangChain Graph Q&A with Neo4j

A project demonstrating how to build a **Question & Answering application over a Neo4j Graph Database** using LangChain and Groq LLM. The project covers basic graph Q&A as well as advanced prompt strategies using few-shot examples and semantic similarity selection.

## Overview

This repository contains two Jupyter notebooks:

| Notebook | Description |
|---|---|
| `Experiements.ipynb` | Build a basic Q&A pipeline over a Neo4j movie graph using `GraphCypherQAChain` and Groq LLM |
| `promptstratergies.ipynb` | Advanced prompt engineering using few-shot examples with `SemanticSimilarityExampleSelector` and FAISS vector store |

The application translates natural language questions into Cypher queries, executes them against a Neo4j graph database, and returns human-readable answers.

## Graph Schema

The project uses a **Movies Graph** dataset with the following schema:

**Nodes:** `Movie`, `Person`, `Genre`, `Country`, `Company`, `Engineer`, `CEO`

**Relationships:**
- `(:Person)-[:ACTED_IN]->(:Movie)`
- - `(:Person)-[:DIRECTED]->(:Movie)`
  - - `(:Movie)-[:IN_GENRE]->(:Genre)`
    - - `(:Engineer)-[:LIVES_IN]->(:Country)`
     
      - ## Tech Stack
     
      - - **[LangChain](https://www.langchain.com/)** — LLM orchestration framework
        - - **[Neo4j](https://neo4j.com/)** — Graph database
          - - **[Groq](https://groq.com/)** — LLM inference (llama-3.3-70b-versatile)
            - - **[FAISS](https://faiss.ai/)** — Vector similarity search for few-shot example selection
              - - **[HuggingFace Embeddings](https://huggingface.co/)** — Sentence embeddings (all-MiniLM-L6-v2)
                - - **[python-dotenv](https://pypi.org/project/python-dotenv/)** — Environment variable management
                 
                  - ## Prerequisites
                 
                  - - Python 3.9+
                    - - A running Neo4j instance (local or [Neo4j Aura](https://neo4j.com/cloud/platform/aura-graph-database/))
                      - - A [Groq API key](https://console.groq.com/)
                       
                        - ## Installation
                       
                        - 1. **Clone the repository**
                          2.    ```bash
                                   git clone https://github.com/Akhilkhana/langchain-neo4j-graph-qa.git
                                   cd langchain-neo4j-graph-qa
                                   ```

                                2. **Create and activate a virtual environment**
                                3.    ```bash
                                         python -m venv .venv
                                         source .venv/bin/activate   # On Windows: .venv\Scripts\activate
                                         ```

                                      3. **Install dependencies**
                                      4.    ```bash
                                               pip install -r requirements.txt
                                               ```

                                            4. **Set up environment variables**
                                        
                                            5.    Create a `.env` file in the root directory:
                                            6.   ```env
                                                    NEO4J_URI=bolt://localhost:7687
                                                    NEO4J_USERNAME=neo4j
                                                    NEO4J_PASSWORD=your_neo4j_password
                                                    GROQ_API_KEY=your_groq_api_key
                                                    ```

                                                 ## Usage

                                                 Launch Jupyter and open either notebook:

                                                 ```bash
                                                 jupyter notebook
                                                 ```

                                                 ### Notebook 1 — Basic Graph Q&A (`Experiements.ipynb`)
                                                 - Connects to Neo4j and loads a movies dataset via CSV
                                                 - - Creates a `GraphCypherQAChain` with Groq LLM
                                                   - - Demonstrates natural language queries like *"Who was the director of the movie Casino?"*
                                                    
                                                     - ### Notebook 2 — Prompt Strategies (`promptstratergies.ipynb`)
                                                     - - Uses 14 curated few-shot question–Cypher pairs
                                                       - - Builds a `SemanticSimilarityExampleSelector` backed by FAISS to inject relevant examples into the prompt
                                                         - - Runs test queries and evaluates the generated Cypher and answers
                                                          
                                                           - ## Example Queries
                                                          
                                                           - ```
                                                             "Who directed the movie Casino?"
                                                             "What movies did Tom Hanks act in?"
                                                             "What are the top 3 movies in the Drama genre?"
                                                             "What genre is Pulp Fiction?"
                                                             "Which movies have an IMDB rating above 8.5?"
                                                             ```

                                                             ## Project Structure

                                                             ```
                                                             .
                                                             ├── Experiements.ipynb         # Basic Graph Q&A notebook
                                                             ├── promptstratergies.ipynb    # Advanced prompt strategies notebook
                                                             ├── requirements.txt           # Python dependencies
                                                             ├── .env                       # Environment variables (not committed)
                                                             └── README.md
                                                             ```

                                                             ## License

                                                             This project is open source and available under the [MIT License](LICENSE).
