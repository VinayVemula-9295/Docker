#Stage:1 
FROM python:3.11-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --upgrade pip && pip install --no-cache-dir -r requirements.txt
COPY app.py .

#Stage:2
FROM gcr.io/distroless/python3-debian11
COPY --from=builder /app /app
WORKDIR /app
CMD ["app.py"]
