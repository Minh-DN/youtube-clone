# Stage 1: Build stage
FROM node:18 AS builder

# Set the working directory in the container 
WORKDIR /app

# Copy package.json and package-lock.json into the working directory
COPY package*.json ./

# Install any required packages as specified in package.json
RUN npm install

# Copy source code to docker image
COPY . .

# Build the app
RUN npm run build

# Stage 2: Production stage
FROM node:18

# Install ffmpeg in the container
RUN apt-get update && apt-get install -y ffmpeg

# Set the working directory in the container 
WORKDIR /app

# Copy package.json and package-lock.json
COPY package*.json ./

# Install only production dependencies
RUN npm install --only=production

# Copy built app from the builder stage
COPY --from=builder /app/dist ./dist

# Make port 3000 available outside this container
EXPOSE 3000 

# Define the command to run your app using CMD (only one CMD allowed)
CMD ["npm", "run", "serve"]





