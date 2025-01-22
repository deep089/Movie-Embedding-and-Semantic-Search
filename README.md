# Movie Embedding and Search Application

A Streamlit-based web application that enables semantic search across IMDB's top 1000 movies using sentence transformers and SQLite for storing embeddings.

## Features

- Semantic search across movie titles and overviews
- Real-time text cleaning and embedding generation
- Persistent storage of embeddings in SQLite database
- Interactive web interface built with Streamlit
- Cosine similarity-based search results
- Top 5 similar movies display

## Prerequisites

```
python >= 3.6
streamlit
pandas
numpy
sqlite3
sentence-transformers
```

## Installation

1. Clone this repository:
```bash
git clone <repository-url>
cd movie-search-app
```

2. Install required packages:
```bash
pip install -r requirements.txt
```

3. Download the dataset:
   - Ensure `imdb_top_1000.csv` is in the root directory
   - The CSV should contain at least `Series_Title` and `Overview` columns

## Usage

1. Start the Streamlit application:
```bash
streamlit run app.py
```

2. The application will:
   - Load and display the initial movie dataset
   - Clean text data automatically
   - Generate embeddings using the MiniLM model
   - Store data in SQLite when requested
   - Provide a search interface for finding similar movies

## Project Structure

- `app.py`: Main application file containing all the code
- `movies.db`: SQLite database storing movie data and embeddings
- `imdb_top_1000.csv`: Source data file

## Key Components

### Data Loading and Caching
- Uses `@st.cache_data` for efficient data loading
- Caches the embedding model using `@st.cache_resource`
- Implements caching for embedding generation

### Text Processing
- Converts text to lowercase
- Removes extra whitespace
- Strips special characters
- Combines title and overview for better semantic matching

### Embedding Generation
- Uses `paraphrase-MiniLM-L6-v2` model
- Generates embeddings for combined text
- Stores embeddings as binary blobs in SQLite

### Search Functionality
- Implements cosine similarity for semantic matching
- Returns top 5 similar movies
- Displays results with titles and overviews

## Database Schema

```sql
CREATE TABLE movies (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    Series_Title TEXT,
    Overview TEXT,
    Embeddings BLOB
)
```

## Future Improvements

1. Add batch processing for large datasets
2. Implement more sophisticated search algorithms
3. Add filtering options (by year, rating, etc.)
4. Include movie metadata in search results
5. Add user feedback mechanism for search results

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Acknowledgments

- IMDB for the movie dataset
- Sentence Transformers for the embedding model
- Streamlit for the web framework
