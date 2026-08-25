Local AI Agent with RAG (LangChain + Ollama + ChromaDB)

What it is:
A locally-hosted, retrieval-augmented question-answering agent, built entirely with open-source tools so it runs with zero cloud API costs and no data leaving the machine. The demo use case is a restaurant Q&A bot: it ingests customer reviews from a CSV, embeds them into a vector database, and lets a user ask natural-language questions (e.g., "How is the pizza's gluten-free crust?") that get answered by an LLM grounded in the most relevant reviews.

How it works:

vector.py — Loads reviews from realistic_restaurant_reviews.csv into pandas, generates embeddings locally using Ollama's mxbai-embed-large model, and persists them in a ChromaDB vector store (OllamaEmbeddings + Chroma from LangChain). Metadata like rating and date is preserved for each entry, and the index is only rebuilt if it doesn't already exist on disk.
main.py — Sets up a LangChain retriever over the vector store, builds a prompt template that injects retrieved reviews as context, and chains it (prompt | model) to a local LLaMA3.2 model served through Ollama. Runs an interactive CLI loop where each user question triggers a similarity search, then a grounded generation step.
