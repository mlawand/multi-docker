#building a production ready copy of the app to be added to the nginx server
FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000
#copying the configutation to the server configuration directory
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf 
#copying from the first builder into the html location on the nginx server
COPY --from=builder /app/build /usr/share/nginx/html