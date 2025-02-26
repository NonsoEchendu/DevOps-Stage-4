# Use Node.js 8 as the base image
FROM node:8-slim

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the port specified in TODO_API_PORT
EXPOSE 8082

# Run the application
CMD ["npm", "start"]