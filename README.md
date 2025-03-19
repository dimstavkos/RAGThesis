# Retrieval-Augmented Airbnb Recomendation System
## Overview
This system is a Retrieval-Augmented Generation (RAG) pipeline designed to provide intelligent Airbnb recommendations based on proximity to Points of Interest (POIs). Users can input natural language queries such as:

"Find Airbnbs within 100 meters of Acropolis Museum"

"Find Airbnbs within 500 meters of a park"

The system extracts key entities from the query (distance, named POI, or POI category), retrieves relevant POIs using vector search, and performs geospatial filtering to return the most relevant Airbnb listings. Finally, a language model summarizes the results for enhanced readability.
