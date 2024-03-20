# Use the official Node.js image as base
FROM node:14 AS builder

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the React app
RUN npm run build

# Use NGINX as the production server
FROM nginx:alpine

# Copy the built React app from the previous stage
COPY --from=builder /app/build /usr/share/nginx/html

# Expose the port the app runs on
EXPOSE 80

# Start NGINX to serve the app
CMD ["nginx", "-g", "daemon off;"]