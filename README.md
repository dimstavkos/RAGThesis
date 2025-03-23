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
**Generated Answer:** \![Alt text](https://raw.githubusercontent.com/dimstavkos/RAGThesis/main/images/Example%201.jpg)\
![Alt text](https://raw.githubusercontent.com/dimstavkos/RAGThesis/main/images/Example%201_2.jpg)\
**Analysis:** The system correctly interprets the user's intent by identifying the specified POI
class ("cafe") and retrieving relevant instances accordingly. The retrieval
process functions as intended, first locating cafes through vector-based search
and subsequently identifying Airbnb listings within a 500-meter radius of each
retrieved cafe. This demonstrates the system's ability to accurately chain
retrieval steps based on spatial proximity and semantic intent.\

### Example 2
**User Query:** “Find Airbnbs 500 meters from a hookah cafe”\
**Generated Answer:** ![Alt text](https://raw.githubusercontent.com/dimstavkos/RAGThesis/main/images/Example%202.jpg)\
**Analysis:** In this case, the system produces no output. Although the underlying database
contains a relevant POI entry (e.g., "hookah cafe"), no Airbnb listings were
found within a 500-meter radius of this location. To investigate whether the
absence of results was due to restrictive spatial constraints, the radius
parameter was subsequently increased to 1000 meters. However, even with
this adjustment, the system still failed to retrieve any nearby Airbnb listings.
This outcome highlights a critical limitation when working with sampled subsets
of the original datasets. Specifically, the reduced data density may lead to
scenarios in which either relevant POIs cannot be retrieved or nearby Airbnbs
are not present in proximity to those POIs. In such cases, adjusting parameters
like the search radius becomes necessary to compensate for the sparsity of the
sample and obtain meaningful results.\

### Example 3
**User Query:** “Find Aribnbs 1500 meters from a bakery”\
**Generated Answer:** \![Alt text](https://raw.githubusercontent.com/dimstavkos/RAGThesis/main/images/Example%203.jpg)\
![Alt text](https://raw.githubusercontent.com/dimstavkos/RAGThesis/main/images/Example%203_1.jpg)\
**Analysis:** In this example, the system correctly identifies that the query targets a specific
POI class ("bakery") and performs as intended. It successfully retrieves top-
ranked instances of the specified class and subsequently presents the Airbnb
listings located in proximity to those POIs. This demonstrates that the retrieval
and generation components are functioning effectively in scenarios where both
relevant POIs and nearby Airbnbs exist within the defined spatial constraints.\

### Example 4
**User Query:** Find Airbnbs 700 meters from Βενέτη”\
**Generated Answer:** ![Alt text](https://raw.githubusercontent.com/dimstavkos/RAGThesis/main/images/Example%204.jpg)\
**Analysis:** In this case, the query targets a specific POI by name, using its Greek-language
representation ("Βενέτης"). The system successfully identifies one matching
instance of the POI and proceeds to retrieve and present the nearby Airbnb
listings within the defined spatial radius. This example illustrates the system's
ability to handle non-English input and perform accurate name-based retrieval,
provided that relevant entries exist in the underlying dataset.\

### Example 5
**User Query:** “Find Airbnbs 800 meters from a Galaxias supermarket”\
**Generated Answer:** ![Alt text](https://raw.githubusercontent.com/dimstavkos/RAGThesis/main/images/Example%205.jpg)\
**Analysis:** In this example, the query uses the Latin-script version of the Greek
supermarket name "Galaxias" instead of its native Greek spelling "Γαλαξίας".
The system interprets "Galaxias" as referring to a general class, likely due to
its semantic association with the word “galaxy” in English or Spanish, and
retrieves Airbnb listings near generic supermarkets rather than specifically near
Γαλαξίας locations. By contrast, when the same query is expressed using the
original Greek spelling, the system correctly treats it as a named entity and
retrieves results accordingly. This behavior can be attributed to the use of the gte-large pretrained
multilingual embedding model from Hugging Face. Although the model
supports multiple languages and is designed for general-purpose retrieval, it
may not reliably connect transliterated names to their original forms unless such
mappings were strongly represented during training. As a result, the embedding
for "Galaxias" does not sufficiently match the embeddings of POIs labeled
"Γαλαξίας" in the dataset, leading to reduced retrieval accuracy. This highlights
a core limitation in multilingual named entity handling, especially in contexts
involving transliteration or language mixing.
Additionally, variations in natural language phrasing were found to influence the
model’s interpretation of query intent. When using an indefinite article—for
example, "Find Airbnbs near a Galaxias supermarket", the model tends to
interpret the phrase as referring to a general class rather than a specific POI.
Consequently, it retrieves Airbnb listings near generic supermarkets. However,
omitting the article, for instance, "Find Airbnbs near Galaxias supermarket",
results in the model treating the phrase more like a named entity, yielding more
accurate and targeted results.
The inclusion of an article such as "a" can shift the embedding vector toward a
more generic semantic space, while the absence of such determiners
emphasizes the named nature of the phrase. These findings highlight the
sensitivity of retrieval performance to natural language phrasing and
underscore the importance of query formulation in achieving precise and
contextually relevant results.\





