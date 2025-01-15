# A/B Testing MongoDB Repository

A Python-based MongoDB repository for managing A/B testing experiments with applicant data. This repository provides tools for assigning applicants to experimental groups, tracking quiz completion rates, and managing email campaigns.



## 🚀 Features

- **Automated Group Assignment**: Randomly assign applicants to control and treatment groups
- **Date-Based Filtering**: Find and process applicants based on application dates
- **Email Campaign Support**: Export treatment group email addresses for campaign management
- **Robust Error Handling**: Comprehensive error checking and validation
- **Type Annotations**: Full Python type hinting support for better code reliability
- **MongoDB Integration**: Seamless integration with MongoDB for data persistence

## 📋 Prerequisites

- Python 3.8+
- MongoDB 4.0+
- pandas
- pymongo

## 🔧 Installation

1. Clone the repository:
```bash
git clone https://github.com/mhadeli/ab-testing.git
cd ab-testing-repo
```

2. Install required packages:
```bash
pip install -r requirements.txt
```

3. Configure MongoDB connection (default: localhost:27017)

## 💻 Usage

### Basic Usage

```python
from mongo_repository import MongoRepository

# Initialize repository
repo = MongoRepository()

# Run experiment for a specific date
result = repo.assign_to_groups("2024-01-01")
print(f"Updated {result['nModified']} records")

# Export treatment group emails
observations = repo.find_by_date("2024-01-01")
export_treatment_emails(observations)
```

### Custom MongoDB Connection

```python
from pymongo import MongoClient

# Create custom client
client = MongoClient(host='your-host', port=27017)

# Initialize repository with custom client
repo = MongoRepository(
    client=client,
    db_name='your-database',
    collection_name='your-collection'
)
```

## 📚 API Reference

### MongoRepository

#### `__init__(client=None, db_name="wqu-abtest", collection_name="ds-applicants")`
Initialize the repository with MongoDB connection settings.

#### `find_by_date(date_string: str) -> List[Dict[str, Any]]`
Find incomplete quiz applicants for a specific date.

Parameters:
- `date_string`: Date in 'YYYY-MM-DD' format

#### `update_applicants(observations: List[Dict[str, Any]]) -> Dict[str, int]`
Update multiple applicant documents in the collection.

Returns:
- Dictionary with counts of matched and modified documents

#### `assign_to_groups(date_string: str) -> Dict[str, int]`
Assign applicants to control and treatment groups.

Returns:
- Dictionary with operation results

### Utility Functions

#### `export_treatment_emails(observations: List[Dict[str, Any]], directory: str = ".")`
Export treatment group email addresses to CSV file.

## 📁 Project Structure

```
ab-testing-repo/
│
├── mongo_repository.py     # Main repository implementation
├── requirements.txt        # Project dependencies
├── README.md              # This file
├── tests/                 # Test files
│   └── test_repository.py
└── examples/              # Example scripts
    └── basic_usage.py
```

## 🧪 Running Tests

```bash
python -m pytest tests/
```

## 📊 Example Data Format

Expected document structure in MongoDB:

```json
{
    "_id": "ObjectId(...)",
    "createdAt": "ISODate(...)",
    "email": "applicant@example.com",
    "admissionsQuiz": "incomplete",
    "inExperiment": true,
    "group": "email (treatment)"
}
```

## 👥 Authors

- Adeli - Initial work - [mhadeli](https://github.com/mhadeli)
