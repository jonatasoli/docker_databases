FROM node:10.15.3-alpine

WORKDIR /user/app

COPY package*.json ./

RUN npm install

COPY .  .

EXPOSE 4000

CMD ["npm", "run", "dev"]
