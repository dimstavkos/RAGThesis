# Retrieval-Augmented Airbnb Recomendation System
## Overview
This system is a Retrieval-Augmented Generation (RAG) pipeline designed to provide intelligent Airbnb recommendations based on proximity to Points of Interest (POIs). Users can input natural language queries such as:

- "Find Airbnbs within 100 meters of Acropolis Museum"

- "Find Airbnbs within 500 meters of a park"

The system extracts key entities from the query (distance, named POI, or POI category), retrieves relevant POIs using vector search, and performs geospatial filtering to return the most relevant Airbnb listings. Finally, a language model summarizes the results for enhanced readability.

## Data Sources

The system integrates the following datasets:

- Airbnb Listings Dataset: Contains Airbnb properties with details such as name, description, and location.

- Points of Interest (POI) Dataset: Includes geographic coordinates and classifications (e.g., museums, parks) of popular locations.

## Installation & Usage (Google Colab)
This system is designed to run in Google Colab, requiring no local installation. To use it:

### 1. Open the Colab Notebook
To run the Retrieval-Augmented Airbnb Recommendation System, simply open the provided Google Colab notebook.

https://colab.research.google.com/drive/1Izrs4T8YyXmWnvjHvTGUaiVnM1NrYzN6?usp=sharing

### 2. Run the Cells
- Install required dependencies using pip (included in the first cell).
- Ensure datasets are stored in Google Drive and are accessible by the notebook.
### 3. Set Up Environment Variables
Create a .env file in Google Drive to store sensitive information like database credentials and API keys.
```bash
MONGO_USERNAME=username
MONGO_PASSWORD=password
MONGO_DB=airbnb_db
HUGGINGFACE_TOKEN=hf_token
```

## Usage
- Input a query via the Colab interface.
- The system extracts the POI name/category and search radius.
- It retrieves POIs via vector search and executes geospatial filtering to find Airbnbs near POI.
- The system will return the filtered Airbnb listings and summarize the results.

> Example: "Find Airbnbs within 100 meters of Acropolis Museum"\
> The system will process the request and return results.


## Answer Generation
### Example 1
**User Query:** "Find Aribnbs 500 meters from a cafe"\
**Generated Answer:** Image\
**Analysis:**\

### Example 2
**User Query:** “Find Airbnbs 500 meters from a hookah cafe”\
**Generated Answer:** Image\
**Analysis:**\

### Example 3
**User Query:** “Find Aribnbs 1500 meters from a bakery”\
**Generated Answer:** Image\
**Analysis:**\

### Example 4
**User Query:** Find Airbnbs 700 meters from Βενέτη”\
**Generated Answer:** Image\
**Analysis:**\

### Example 5
**User Query:** “Find Airbnbs 800 meters from a Galaxias supermarket”\
**Generated Answer:** Image\
**Analysis:**\





