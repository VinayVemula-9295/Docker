
FROM node:18-alpine AS builder
WORKDIR /app
COPY . .
RUN npm install --omit=dev

FROM gcr.io/distroless/nodejs18
COPY --from=builder /app /app
WORKDIR /app
CMD ["index.js"]
