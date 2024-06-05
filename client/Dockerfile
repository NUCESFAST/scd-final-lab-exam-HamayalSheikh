# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory
WORKDIR /usr/src/1125_frontend

# Copy package.json and package-lock.json files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Build the app
RUN npm run build

# Install serve to serve the build files
RUN npm install -g serve

# Expose the port serve runs on
EXPOSE 1125

# Command to run the app
CMD ["serve", "-s", "build"]
