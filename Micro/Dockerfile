# Stage 1: Build React app
FROM node:18-alpine AS build
WORKDIR /app

# Install dependencies (better caching)
COPY package*.json ./
RUN npm ci --silent

# Copy code and build
COPY . .
RUN npm run build

# Stage 2: Serve with nginx
FROM nginx:stable-alpine

# Copy build output directly (No manual cleanup needed)
COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]