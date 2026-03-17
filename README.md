#  NestNav: AI-Powered Apartment Finder Virtual Assistant

**CMPE 259 – NLP Project | San José State University**  
**Author:** Latha Boralingaiah (018301361)

---

##Project Overview

NestNav is an LLM-based virtual assistant designed to help users find rental housing. It tackles the challenge of navigating thousands of listings across multiple platforms by providing customized recommendations, price comparisons, neighborhood analysis, and real-time market insights.

The project demonstrates **LLM tool-calling capabilities** by integrating database lookup tools and web search tools that the model invokes autonomously based on user queries.

### Target Users
- Students seeking housing near campus
- Young professionals relocating for work
- Budget-conscious renters
- Anyone searching for apartments

---

##  Current Status: Phase 1 – Project Setup & Data Exploration

### What has been completed so far

- Finalized the project idea and submitted the project proposal
- Selected two LLMs for comparison:
  - **Phi-3.5-mini-instruct** (3.8B params) – smaller model, FP16
  - **Mistral-7B-Instruct-v0.3** (7B params) – larger model, 4-bit quantization
- Downloaded the [USA Housing Listings (Craigslist) dataset from Kaggle](https://www.kaggle.com/datasets/austinreese/usa-housing-listings)
- Created a Google Colab notebook for initial exploration
- Performed initial data filtering and parsing to understand the dataset schema (columns include price, region, housing type, beds, baths, sqfeet, lat/long, pets, laundry, parking, description)
- Researched LLM tool-calling and function-calling patterns, including ReAct-style prompting and how Phi-3.5 and Mistral handle structured tool definitions
- Explored how to set up a SQLite-based lookup tool for querying the housing dataset during conversations
- Defined 20 example user queries covering apartment search, rent comparison, neighborhood analysis, commute, and budgeting

### What is currently in progress

- Cleaning and preprocessing the dataset (handling missing values in price/location, removing duplicates, normalizing region names)
- Testing Phi-3.5-mini-instruct in Google Colab to verify basic prompt-response behavior
- Designing tool JSON schemas for the function-calling pipeline (search_apartments, compare_rent, get_neighborhood_info)

---

##  Dataset

**Source:** [USA Housing Listings (Craigslist) – Kaggle](https://www.kaggle.com/datasets/austinreese/usa-housing-listings)

Key fields in the dataset:

| Field | Description |
|-------|-------------|
| `price` | Monthly rent in USD |
| `region` | Craigslist region (e.g., Sacramento, San Jose) |
| `type` | Housing type (apartment, condo, house, etc.) |
| `beds` / `baths` | Bedroom and bathroom count |
| `sqfeet` | Square footage |
| `cats_allowed` / `dogs_allowed` | Pet policy |
| `laundry_options` | Laundry type (in-unit, shared, none) |
| `parking_options` | Parking availability |
| `lat` / `long` | Geolocation coordinates |
| `description` | Free-text listing description |

---

## Folder Structure

```
nestnav/
├── README.md                        # Project documentation
├── requirements.txt                 # Python dependencies
├── .gitignore                       # Git ignore rules
│
├── data/
│   └── raw/                         # Original Kaggle dataset (not committed)
│       └── housing.csv
│
├── notebooks/
│   └── 01_eda.ipynb                 # Exploratory Data Analysis (in progress)
│
└── docs/
    └── project_proposal.pdf         # Submitted proposal document
```

> **Note:** Additional folders for `src/`, `configs/`, `tests/`, and `data/processed/` will be added in later phases as the tool-calling pipeline and evaluation framework are built.

---

## Getting Started

### Prerequisites
- Python 3.10+
- Google Colab (recommended for GPU access)
- Kaggle account (for dataset download)

### Setup

```bash
# Clone the repository
git clone https://github.com/<your-username>/NestNav-AI-Powered-Apartment-Finder-Virtual-Assistant.git
cd NestNav-AI-Powered-Apartment-Finder-Virtual-Assistant

# Install dependencies
pip install -r requirements.txt

# Download dataset from Kaggle
# Option 1: Manual download from the Kaggle link above, place housing.csv in data/raw/
# Option 2: Using Kaggle CLI
kaggle datasets download -d austinreese/usa-housing-listings -p data/raw/ --unzip
```

---

## LLM Models (Selected)

| Model | Parameters | Role | Justification |
|-------|-----------|------|---------------|
| **Phi-3.5-mini-instruct** | 3.8B | Smaller model | Microsoft's compact model with excellent instruction-following |
| **Mistral-7B-Instruct-v0.3** | 7B | Larger model | State-of-the-art 7B model, 4-bit quantization fits Google Colab |

---

##  Example User Queries (Defined)

| # | Query |
|---|-------|
| 1 | Find 2-bedroom apartments in Sacramento for under $2500 |
| 2 | What's the average rent for 1BR in Jacksonville? |
| 3 | Compare rent prices: San Jose vs Sacramento |
| 4 | Pet-friendly apartments in Sacramento |
| 5 | Is this neighborhood safe? |
| 6 | Apartments with in-unit laundry |
| 7 | What's the commute time to downtown Columbus? |
| 8 | Show me safest neighborhoods under $2000 |
| 9 | Apartments with parking included |
| 10 | Compare walk scores of these two areas |
| 11 | What amenities are common in this area? |
| 12 | Is rent going up or down in Columbus? |
| 13 | Find apartments near bus/train stations |
| 14 | What's typically included in rent? |
| 15 | Best neighborhoods for young professionals |
| 16 | Find month-to-month lease options |
| 17 | What questions should I ask the landlord? |
| 18 | Calculate total monthly cost with utilities |
| 19 | Studios vs 1-bedroom price difference? |
| 20 | Create apartment checklist for my budget |

---

##  License

This project is for academic purposes as part of CMPE 259 at San José State University.

---

## Acknowledgments

- Dataset: [Austin Reese – USA Housing Listings (Kaggle)](https://www.kaggle.com/datasets/austinreese/usa-housing-listings)
- Models: [Microsoft Phi-3.5](https://huggingface.co/microsoft/Phi-3.5-mini-instruct), [Mistral AI](https://huggingface.co/mistralai/Mistral-7B-Instruct-v0.3)
- San José State University – CMPE 259 NLP Course
