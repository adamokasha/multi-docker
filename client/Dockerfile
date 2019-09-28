FROM node:alpine as builder
WORKDIR '/app'
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
# instruction for us (as developers) AND elastic beanstalk. 
# This in most cases does nothing.
EXPOSE 3000

# copy nginx conf file
COPY ./nginx/default/conf /etc/nginx/conf.d/default.conf

# copy build dir to nginx default serving directory
COPY --from=builder /app/build /usr/share/nginx/html