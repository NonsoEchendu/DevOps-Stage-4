# Stage 1: Build the Vue.js app
FROM node:14 AS build-stage

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install  

# Copy the rest of the application code
COPY . .

# Build the Vue.js app for production
RUN npm run build  

# Stage 2: Serve the app using Node.js
FROM node:14 AS production-stage

# Set the working directory
WORKDIR /app

# Copy the built app from the build stage
COPY --from=build-stage /app/dist ./dist

# Copy package.json and install only production dependencies
COPY package*.json ./
RUN npm install --only=production

# Copy the .env file from root directory
COPY ../.env .

# Expose port
EXPOSE 8080

# Start the app using a Node.js server
CMD ["npm", "run", "dev"]