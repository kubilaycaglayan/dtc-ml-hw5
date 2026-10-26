# ML Zoomcamp 2026 — Homework 5: Deployment

Local worked solution using the course's frozen lead-scoring model release. The checked-in API, model helper, Dockerfile, dependency lock, metadata, defaults, and `pipeline.bin` are the canonical files from the course homework. The model artifact SHA-256 is verified in the notebook.

## Answers

| Question | Answer |
|---|---|
| 1 | Local `uv` version is recorded in the notebook (setup check; not graded). |
| 2 | Scikit-Learn **1.7.2** |
| 3 | Conversion probability **0.533** |
| 4 | API conversion probability **0.770** |
| 5 | Docker base image `python:3.11.15-slim-bookworm` |
| 6 | Container conversion probability **0.770** |

## Set up the reference environment

The homework pins Python 3.11.15 and uses `uv`:

```bash
uv sync --locked
uv run --locked python smoke_test.py
```

To open and run the explanatory notebook, install its optional notebook tools into the same environment and register the kernel:

```bash
uv pip install --python .venv/bin/python -r requirements-notebook.txt
.venv/bin/python -m ipykernel install --user --name mlzoomcamp-hw5 --display-name 'Python (ML Zoomcamp HW5)'
.venv/bin/jupyter lab homework_05_solutions.ipynb
```

The notebook runs the local API and Docker checks in their respective sections. Docker must be installed and running for Question 6.

## Run the API manually

```bash
uv run --locked uvicorn predict:app --host 0.0.0.0 --port 9696
```

In another terminal, use `curl` or `uv run --locked python q6_test.py` to call it.

## Build and run the container manually

```bash
docker build -t zoomcamp-model:2026-hw5 .
docker run --rm -p 9696:9696 zoomcamp-model:2026-hw5
```

Then call `http://localhost:9696/health` and `http://localhost:9696/predict`.

The upstream assignment and frozen release are in [DataTalksClub's HW5 folder](https://github.com/DataTalksClub/machine-learning-zoomcamp/tree/main/cohorts/2026/homework/05-deployment).
