FROM node:18.9.1

WORKDIR /app

COPY package.json .

RUN npm install

EXPOSE 5050

COPY . .

CMD ["npm", "start"]
