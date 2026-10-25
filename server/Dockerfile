FROM node:18-alpine

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Expose port
EXPOSE 5000

# Health check - Just check if server is running (don't query DB)
HEALTHCHECK --interval=15s --timeout=10s --start-period=10s --retries=5 \
    CMD node -e "require('http').get('http://localhost:5000', (r) => {if (r.statusCode !== 404) throw new Error(r.statusCode)})"

# Start the server
CMD ["npm", "start"]

