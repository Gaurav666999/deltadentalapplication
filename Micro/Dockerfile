##############

# Stage 1: Build React app
FROM node:18-alpine AS build
WORKDIR /app

# Install dependencies
COPY package*.json ./
RUN npm ci

# Copy rest of code
COPY . .

# Build app
RUN npm run build

# Stage 2: Serve with nginx
FROM nginx:alpine

# Remove default nginx static config
RUN rm -rf /usr/share/nginx/html/*

# Copy build output - Verify if your app builds to /app/build or /app/dist
COPY --from=build /app/build /usr/share/nginx/html

# Copy custom nginx config
# This expects nginx.conf to be in the same folder as this Dockerfile
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
