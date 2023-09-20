# build env
FROM node:13.12.0-alpine as build 
WORKDIR /app 
COPY package*.json ./ 
RUN npm install && \
    npm run build && \
    cp -r build result_build
COPY . ./ 
CMD ["npm", "start"]