# Retrieval-Augmented Airbnb Recomendation System
## Overview
This system is a Retrieval-Augmented Generation (RAG) pipeline designed to provide intelligent Airbnb recommendations based on proximity to Points of Interest (POIs). Users can input natural language queries such as:

- "Find Airbnbs within 100 meters of Acropolis Museum"

- "Find Airbnbs within 500 meters of a park"

The system extracts key entities from the query (distance, named POI, or POI category), retrieves relevant POIs using vector search, and performs geospatial filtering to return the most relevant Airbnb listings. Finally, a language model summarizes the results for enhanced readability.

## Data Sources

The system integrates the following datasets:

- Airbnb Listings Dataset: Contains Airbnb properties with details such as name, description, and location.

- Points of Interest (POI) Dataset: Includes geographic coordinates and classifications of popular locations.

## Installation & Usage (Google Colab)
This system is designed to run in Google Colab, requiring no local installation. To use it:

### 1. Open the Colab Notebook

### 2. Run the Cells
- Follow the notebook instructions.
- Install required dependencies using pip (included in the first cell).
- Ensure datasets are stored in Google Drive and are accessible by the notebook.
### 3. Set Up Environment Variables
Create a .env file in Google Colab to store sensitive information like database credentials and API keys.
> MONGO_USERNAME=username
MONGO_PASSWORD=password
MONGO_DB=airbnb_database
HUGGINGFACE_TOKEN=hf_token
Input a Query

Example: "Find Airbnbs within 100 meters of Acropolis Museum"
The system will process the request and return results.

