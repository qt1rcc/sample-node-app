# Create image based on the official Node image from dockerhub
FROM node:hydrogen AS development

# Create app directory
WORKDIR /usr/src/app

# Copy dependency definitions
COPY package.json /usr/src/app
COPY package-lock.json /usr/src/app

# Install dependecies
#RUN npm set progress=false \
#    && npm config set depth 0 \
#    && npm i install
RUN npm install

RUN npm ci

# Get all the code needed to run the app
COPY . /usr/src/app

RUN npm run build

# production environment
FROM nginx:stable-alpine
COPY --from=development /usr/src/app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]