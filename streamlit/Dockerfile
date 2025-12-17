FROM python:3.12-slim
WORKDIR /app

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*

# copy from repo-root context
COPY streamlit/requirements.txt ./requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY streamlit/app.py ./app.py

RUN mkdir -p /app/data

HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
  CMD sh -c 'curl -f http://localhost:${PORT:-8501}/_stcore/health || exit 1'

CMD ["sh", "-c", "streamlit run app.py --server.address=0.0.0.0 --server.port=${PORT:-8501}"]
