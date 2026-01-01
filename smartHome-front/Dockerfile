# Stage 1: Build Angular app
FROM node:18-alpine AS builder
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Build the Angular app
RUN npm run build --prod

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Copy custom nginx config (optional)
# COPY nginx.conf /etc/nginx/nginx.conf

# Copy built Angular app from builder stage
COPY --from=builder /app/dist/smart-home /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
