# # frontend/Dockerfile

# # Stage 1: Build React application
# FROM node:16-alpine as build

# WORKDIR /app

# COPY package.json package-lock.json ./
# RUN npm install

# COPY . .
# RUN npm run build

# # Stage 2: Serve the built React app with Traefik labels
# FROM scratch

# # Copy built React app from the build stage
# COPY --from=build /app/build /app/build

# # Traefik labels for routing
# # LABEL "traefik.http.routers.my-frontend.rule"="Host(`your-domain.com`)"  # Replace with your domain
# # LABEL "traefik.http.services.my-frontend.loadbalancer.server.port"="80"
# LABEL "traefik.http.routers.my-frontend.rule"="Host(`your-domain.com`) && PathPrefix(`/`)"
# LABEL "traefik.http.services.my-frontend.loadbalancer.server.port"="80"


# # frontend/Dockerfile -a
# FROM node:16-alpine as build

# WORKDIR /app

# # Install git
# RUN apk add --no-cache git

# COPY package.json package-lock.json ./
# RUN npm install

# COPY . .
# RUN npm run build

# # Debugging step: List the contents of the build directory to ensure it exists
# RUN ls -al /app/dist

# FROM nginx:alpine
# COPY --from=build /app/dist /usr/share/nginx/html
# EXPOSE 80

# CMD ["nginx", "-g", "daemon off;"]


FROM node:16 AS build

# Set the working directory
WORKDIR /app

# Copy the package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Build the application
RUN npm run build

# Use the official Nginx image for serving the frontend
FROM nginx:alpine

# Copy the build output to the Nginx HTML directory
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]

