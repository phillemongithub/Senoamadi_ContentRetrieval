# Intelligent Content Retrieval System

An end-to-end semantic search system that scrapes web content, generates embeddings, and enables natural language queries using vector similarity search.

## Project Overview

This system implements a complete pipeline for:

- **Web Scraping**: Ethically extracting content from 5 diverse sources
- **Text Processing**: Chunking and cleaning text data
- **Embedding Generation**: Creating semantic vectors using transformer models
- **Vector Database**: Storing embeddings in ChromaDB
- **Semantic Search**: Querying content using natural language

## Architecture

```
Web Sources → 
            Scraper → 
                    Text Processor → 
                                    Embedding Generator → 
                                                         Vector DB →
                                                                     Search Interface
```

### Components:

1. **WebScraper**: Handles ethical web scraping with rate limiting
1. **TextProcessor**: Cleans and chunks text into optimal sizes
1. **EmbeddingGenerator**: Creates semantic embeddings using sentence-transformers
1. **VectorDatabase**: ChromaDB implementation for efficient similarity search
1. **SemanticSearchEngine**: Natural language query interface

## Requirements

- Python 3.8 or higher
- 4GB RAM minimum
- Internet connection for scraping
- ~500MB disk space for models and data

## Installation

### Step 1: Clone or Download

```bash
# Create project directory
mkdir content_retrieval_system
cd content_retrieval_system
```

### Step 2: Create Virtual Environment

```bash
# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On Mac/Linux:
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

### Step 4: Download Spacy Model

```bash
python -m spacy download en_core_web_sm
```

## Usage

### Running the Complete System

1. **Open Jupyter Notebook**:

```bash
jupyter notebook content_retrieval_system.ipynb
```

1. **Run All Cells**: Execute cells sequentially from top to bottom
1. **View Results**: Check the output after each section

### Quick Start Code

```python
# Initialize components
from content_retrieval_system import *

# Scrape websites
scraper = WebScraper(CONFIG)
content = scraper.scrape_all()

# Process text
processor = TextProcessor()
chunks = processor.process_all(content)

# Generate embeddings
embedder = EmbeddingGenerator('all-MiniLM-L6-v2')
embeddings, metadata = embedder.generate_embeddings(chunks)

# Setup vector database
db = VectorDatabase()
db.add_documents(embeddings, metadata)

# Search
search = SemanticSearchEngine(db, embedder.model)
results = search.search("What is machine learning?")
search.display_results(results)
```

## Example Queries

Test the system with these example queries:

```python
queries = [
"What is artificial intelligence?",
"How does neural network training work?",
"Latest technology news",
"Python programming basics",
"Scientific research methods"
]

for query in queries:
results = search_engine.search(query, top_k=5)
search_engine.display_results(results)
```

## System Statistics

After running, the system provides:

- Total websites scraped
- Number of text chunks created
- Embedding dimensions and count
- Database statistics
- Search performance metrics

## Customization

### Change Embedding Model

Edit `config.yaml`:

```yaml
embeddings:
model_name: "all-mpnet-base-v2" # For higher quality
```

### Adjust Chunk Size

```yaml
text_processing:
chunk_size: 201 # Increase for longer chunks
chunk_overlap: 150
```

### Add More Websites

```yaml
websites:
- url: "https://secure-web.cisco.com/192Fj87KSt8t9L0dKxdYincNNNubEnuH8bJALZdXuORccj8F8MMZ_8ZwzWBW997xAEfU6gItPIzZknKgfTfYpQtJfYgBtaa0_ELcGuFTGFHSmL6UcG7KMyw4Eo2EXPB-eFRkX4FKLVLn_DlQEeZcbrJ808qXvj7okJ7BsIar1leaQgFPPMusl6CVP3dsgZgKEiKA0wjnWrz8y2z7ypEmqn4f2W_wFB0uXQLXn6CP0Q-vBMlDdKjmTgXbJQlyTTCWGHEt3rG75Dx-4lyRn46laz6fQ3o7ySycPd_AM2cbirrvGeKLUvqTfu8PHkQ79lhJFc0lBPY-VG7gI8WZnEOgj0A/https%3A%2F%2Fyour-website.com"
category: "Your Category"
name: "Website Name"
```

## Project Structure

```
content_retrieval_system/
├── content_retrieval_system.ipynb # Main implementation
├── requirements.txt # Python dependencies
├── config.yaml # Configuration file
├── README.md # This file
├── screenshots/ # Screenshot folder
│ ├── scraping_process.png
│ ├── data_processing.png
│ ├── vector_database.png
│ └── search_results.png
└── system_results.json # Output data (auto-created)
```

## Troubleshooting

### Import Errors

```bash
# Reinstall packages
pip install --upgrade -r requirements.txt
```

### Scraping Fails

- Check internet connection
- Verify website is accessible
- Adjust rate_limit_delay in config
- Try alternative websites
- Making sure we have a minimum of 5000 texts

### Memory Issues

- Reduce batch_size in config
- Process fewer websites initially
- Use smaller embedding model

### ChromaDB Errors

```bash
# Clear database and restart
rm -rf chroma_db/
```

## Performance

Expected performance on standard hardware:

- **Scraping**: ~50 seconds for 4 websites
- **Processing**: ~30 seconds for 201+ chunks
- **Embedding**: ~1-2 minutes for 201 chunks
- **Search**: <1 second per query
