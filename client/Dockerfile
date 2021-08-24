# Start of the build phase
FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . . 
RUN npm run build

# /app/build <-- where all the stuff we care about!

#Start of the run phase
FROM nginx 

#Tells us where to port map to
EXPOSE 3000

# Copy new default nginx config file
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy something from another phase (build phase) to another folder 
COPY --from=builder /app/build /usr/share/nginx/html
