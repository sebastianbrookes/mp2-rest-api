# MP2: Data Processing REST API

A FastAPI application that exposes the MP1 data-cleaning pipeline over HTTP.
Clients upload a CSV with `POST /upload`, which stores the data in memory
and returns an ID. `GET /datasets/{id}` returns rows (with an optional
`limit`). `POST /datasets/{id}/process` validates and cleans the dataset
using the reused MP1 modules in `data_pipeline/` (duplicate removal,
missing-value handling, outlier removal) and returns a cleaning report.
`GET /health` reports status and version. Request-logging middleware gives
each request an `X-Request-ID` header and logs its method, path, status, and
duration. Pytest tests in `tests/` cover upload, the process/retrieve
workflow, and missing datasets.

## Usage

```bash
uvicorn main:app --reload   # then open http://127.0.0.1:8000/docs
python -m pytest tests -v
```
