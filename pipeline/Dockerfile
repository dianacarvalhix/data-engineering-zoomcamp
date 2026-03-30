FROM python:3.13.11-slim

# Copy uv binary from official uv image (multi-stage build pattern)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

WORKDIR /code
COPY pyproject.toml .python-version uv.lock ./
RUN uv sync --locked

RUN pip install pandas pyarrow
#ENV PATH="/code/.venv/bin:$PATH"  ####if uncomment this take out uv run from entrypoint

COPY ingest_data.py .

ENTRYPOINT ["uv", "run", "python","ingest_data.py"]