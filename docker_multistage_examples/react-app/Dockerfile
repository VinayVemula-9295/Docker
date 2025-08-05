##step 1:buildstage 
FROM node:18-alpine as builder

WORKDIR /app

COPY package.json .
COPY package-lock.json .

RUN npm install 

COPY . .

RUN npm run build

##step 2 : serve with nginx

FROM nginx:alpine

COPY --from=builder /app/dist  /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

