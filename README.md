# COVID-19 Data Pipeline
## Project Overview
- This data engineering project ingests COVID-19 historical tracking data from the COVID - - Tracking Project API, processes it using DBT, and generates summary reports.


### Tools and Rationale

- Python: Flexible data processing and API interaction
- SQLAlchemy: Database connectivity and ORM
- DBT: Data transformation and testing
- PostgreSQL: Robust relational database for data storage
- Docker: Containerized, reproducible environment

## Key Components

- API Ingestion: Retrieves state and daily COVID-19 data
- Data Transformation: Uses DBT for data validation and modeling
- Summary Generation: Creates CSV files with state-level infection percentages

### Setup and Running the Project
**Prerequisites**

- Docker
- Docker Compose

### Installation Steps

- Clone the repository
- Build the Docker containers:
`docker-compose build`

### Start the services:
`docker-compose up -d`

### Run data ingestion:
`docker-compose exec python-dbt python src/api_ingest.py`

### Run DBT transformations:
`docker-compose exec python-dbt dbt run --profiles-dir .`

### Generate summaries:
`docker-compose exec python-dbt python src/summary_generator.py`


## Error Handling and Considerations

- Implemented exponential backoff for API request retries
- Rate limit handling for COVID Tracking Project API
- Logging and error tracking

### Output
Summaries are generated in the `outputs/` directory with state-specific infection percentage CSVs.
### Testing
Run DBT tests to validate data integrity:

`docker-compose exec python-dbt dbt test`
