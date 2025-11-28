# Use Node.js official image
FROM node:14

# Set working directory
WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy application source code
COPY . .

# Expose port (Matches server.js port)
EXPOSE 8080

# Start the server
CMD ["node", "server.js"]
