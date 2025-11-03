# VITALE-AI
An AI-driven tool designed to empower biomedical discovery by turning complex literature and data into clear, actionable insights through intelligent exploration.

## Overview

VITALE-AI is a web-based semantic search and analysis platform tailored for biomedical researchers. It goes beyond keyword-based search to understand biological meaning, connections, and trends across thousands of scientific publications. By integrating advanced AI techniques — such as topic modeling, citation analysis, and Gene Ontology classification — VITALE-AI helps users discover high-impact research and uncover hidden relationships within biomedical literature.


## How VITALE-AI Works

The system processes both user-submitted queries and lab-generated experimental data to retrieve relevant literature and insights:

1. **Data Input**  
   - Queries from biologists (e.g., "cytokine signaling in T-cells").
   - Experimental data (e.g., genes, proteins, RNA-seq).

2. **NER & Ontology Classification**  
   - Extracts biological entities using Named Entity Recognition (NER).
   - Classifies entities using Gene Ontology (MF, BP, CC).

3. **Literature Retrieval**  
   - Uses both PubMed search and GO-term associations.
   - Applies semantic similarity for enhanced accuracy.

4. **Semantic NLP Ranking**  
   - Ranks results by relevance, context, and citation impact.

5. **AI-Powered Summarization**  
   - Generates concise, structured outputs with entity relationships.

6. **Output**  
   - Curated articles + GO-tagged insights + intelligent suggestions.

![high level workflow](https://github.com/user-attachments/assets/fa084562-e9bc-4ff0-ab8f-96115fb7b4b5)

*Figure 1: High-Level VITALE-AI Workflow*


## What You Can Do with VITALE-AI

- **AI-powered search**: Input natural language queries and get semantically relevant PubMed articles.
- **Explore insights**: Understand key topics, GO terms, citation links, and publication impact.
- **Visualize connections**: Semantic graphs and clusters show how research is interlinked.
- **Upload your data**: Compare your experimental results against literature to find relevant biological pathways.
- **Summarize with AI**: Let AI synthesize findings and support your research questions.
- **Discover Trends**: Analyze topic evolution, GO category distribution, and high-impact publications in your field of interest.


![Uploading high level workflow.svg…]()

## Project Status

| Feature                          | Status          |
|----------------------------------|-----------------|
| Semantic search backend          | ✅ Completed     |
| Graph-based insights             | ✅ Completed     |
| Experimental data upload         | 🔄 In progress   |
| AI summarization & interaction   | ⏳ Coming soon   |
| User interface (frontend)        | 🔄 Prototype     |

## Type

This is a **research prototype**, currently under development for use in biomedical research labs, academic projects, and innovation pilots.


## Core Technologies

- **NLP & AI**: BioBERT, JNLPBA, GPT-4 (planned), NER, entity normalization, LDA
- **Big Data**: Apache Spark, GraphFrames, Parquet (converted from 100GB+ XML)
- **Biological Knowledge**: Gene Ontology (GO), MeSH terms, chemicals, keywords
- **Citation Intelligence**: PubMed Citation API (elink), custom enrichment
- **Frontend (planned)**: React-based app with tabs: Search | Upload | Summarize | Settings

---

## Frontend UX/UI

The interface includes:

- **Search page** with filters (year, keywords, topics), similarity scoring, and GO-tag annotations.
- **Semantic graph viewer** to explore how publications are linked.
- **Upload tab** to preview and compare your biological data.
- **Summarization tab** with a mock ChatGPT-style assistant.
- **User pages**: Profile, settings (dark/light mode), and experimental toggles.

---

📂 Notebooks Overview
This repository includes modular notebooks that power the VITALE-AI backend:

## **PUBMED_BIGDATA.ipynb**

This repository contains a Jupyter Notebook demonstrating **Exploratory Data Analysis (EDA)** on a PubMed dataset using **PySpark**. The notebook provides a starting point for conducting in-depth EDA on PubMed data and can be easily customized for specific research or analysis tasks. It includes:

- **Data Loading and Preprocessing:**
  - Loading PubMed data from a Parquet file.
  - Parsing nested JSON structures within the data.
  - Handling missing values and data cleaning.
  
- **EDA on Key Features:**
  - Analyzing the distribution of references across articles.
  - Identifying top journals based on article counts.
  - Exploring the distribution of languages used in publications.
  - Examining grant information and funding patterns.
  - Analyzing publication types, chemicals, keywords, and MeSH headings associated with articles.
  
- **Citation Analysis:**
  - Retrieving citation data using the PubMed API.
  - Integrating citation counts with the main dataset.
  - Analyzing citation patterns and distribution.

- **Journal Analysis:**
  - Identifying top journals based on article counts.
  - Tokenizing and normalizing journal names for analysis.
  - Extracting top chemical terms, keywords, and MeSH headings.

> You can explore this notebook at `/notebooks/PUBMED_BIGDATA.ipynb`.


## **PUBMED_GENEONTOLOGY.ipynb**

This notebook performs Gene Ontology (GO) classification on biological entities extracted from PubMed data. It enables semantic tagging of biomedical content for downstream filtering and query enrichment.

- **GO Term Extraction:**
   Loads cleaned PubMed dataset with abstract and keyword tokens.
   Identifies potential biological entities from tokens.
   Extracts GO term matches using go-basic.obo ontology data.
- **Classification and Tagging:**
Categorizes matched terms under BP (Biological Process), MF (Molecular Function), and CC (Cellular Component).
Uses explode, filter, and join operations to associate terms with documents.
Calculates per-article counts for each GO class.
- **Output Preparation:**
Produces a GO-enriched dataset suitable for search and summarization tasks.
Supports ranking and categorization of papers based on biological roles.
Provides .show() previews for validation.

📍 Located at: /notebooks/PUBMED_GENEONTOLOGY.ipynb

## **PUBMED_GRAPHFRAMES.ipynb**

This notebook constructs and analyzes semantic graphs using GraphFrames to explore biomedical publication networks.

- **Environment Setup:**
Installs and configures GraphFrames within Colab using Apache Spark 3.5.0.
Sets up required environment variables and dependencies.
Initializes Spark session with GraphFrames package.
- **Graph Construction:**
Defines vertices (papers, authors, terms) and edges (citations, co-occurrence).
Builds paper–paper graphs based on shared MeSH terms or authorship.
Constructs keyword–paper bipartite graphs to explore topic proximity.
- **Graph Analytics:**
Applies PageRank and label propagation to identify influential nodes.
Computes connected components to detect topic communities.
Adds semantic_score attributes to edges based on frequency and citation impact.

📍 Located at: /notebooks/PUBMED_GRAPHFRAMES.ipynb

## **FINAL_PART_PUBMED.ipynb**
This notebook brings together all modules into a unified semantic retrieval pipeline powered by NLP and GO categorization.
- **Vectorization and Topic Modeling:**
Applies CountVectorizer to generate token frequency matrices.
Uses IDF to compute term weights and highlight unique content.
Performs LDA (Latent Dirichlet Allocation) to extract topics from abstracts.
- **Relevance Scoring & Retrieval:**
Matches user/experimental queries with preprocessed PubMed abstracts.
Ranks articles based on cosine similarity with topic vectors.
Incorporates citation counts and GO term alignment for improved ranking.
- **Output Formatting:**
Generates a ranked list of documents for each query.
Supports integration with UI modules and summarization systems.
Displays results using .show() for real-time inspection.

📍 Located at: /notebooks/FINAL_PART_PUBMED.ipynb


---

## Try It in Colab

> Development notebooks and backend demos are located in `/notebooks`.  
> Notebooks include: semantic search engine, LDA modeling, GO classification, graph construction with GraphFrames, and data parsing from PubMed XML.



## Tech Stack

- **Python**, **PySpark**, **GraphFrames**, **Google Colab**
- **PubMed Data** (cleaned XML → tokens, metadata, MeSH, GO terms)
- **LDA Topic Modeling** and MeSH keyword grouping
- **Gene Ontology Categorization**: BP, MF, CC per matched term
- **Semantic Graph Construction**: based on shared tokens, citations, co-authorship, or GO proximity
- **Planned Frontend**: React-based UI (tabs: search, upload, summarize, settings)


## 📄 License


---

