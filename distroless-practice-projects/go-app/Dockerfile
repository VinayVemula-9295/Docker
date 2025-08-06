
FROM golang:1.21 as builder
WORKDIR /app
COPY main.go .
RUN go build -o app

FROM gcr.io/distroless/static
COPY --from=builder /app/app /app/app
CMD ["/app/app"]
