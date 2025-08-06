Stage:1

FROM node:18-alpine AS builder

WORKDIR /app

COPY . .

RUN npm install --omit=dev


stage 2 :

FROM gcr.io/distroless/nodejs18

COPY --from=builder /app /app

WORKDIR /app

CMD ["index.js"]
