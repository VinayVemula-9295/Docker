#step 1 install dependencies

FROM node:18-alpine as builder

WORKDIR /app

COPY package*.json .

RUN npm ci

#step 2  copy source and run 

FROM node:18-alpine

WORKDIR /app

COPY . .

COPY --from=builder /app/node_modules  ./node_modules
 
EXPOSE 3000

CMD ["node", "server.js"]



