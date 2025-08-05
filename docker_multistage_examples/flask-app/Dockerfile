FROM python:3.11-slim as builder

WORKDIR /app

COPY pyproject.toml poetry.lock ./

RUN pip install poetry && poetry config  virtualenvs.create false && poetry install --no-dev

##stage 2 

FROM python:3.11-slim

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.11  /usr/local/lib/python3.11
COPY --from=builder /usr/local/bin /usr/local/bin

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
