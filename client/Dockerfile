#Base IMage

#FROM node:22-alpine AS builder

#Working Direcotry
#WORKDIR /app

#COPY source code to container working directory
#COPY . .

#INstalling dependencies
#RUN npm install

#Building the app
#RUN npm run build

#Using the Slim image to run ---------------------------------
#FROM node:22-slim

#Working Directory
#WORKDIR /app

#COPY --from=builder /app/node_modules ./node_modules
#COPY --from=builder /app/dist ./dist

#CMD ["npm", "start"]

#Base IMage

#FROM node:22-alpine AS builder

#Working Direcotry
#WORKDIR /app

#COPY source code to container working directory
#COPY . .

#INstalling dependencies
#RUN npm install

#Building the app
#RUN npm run build

#Using the Slim image to run ---------------------------------
#FROM node:22-slim

#Working Directory
#WORKDIR /app

#COPY --from=builder /app/node_modules ./node_modules
#COPY --from=builder /app/dist ./dist

#CMD ["npm", "start"]

# Build stage
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy source code
COPY . .

# Build the React app
RUN npm run build

# Production stage
FROM node:18-alpine

WORKDIR /app

RUN npm install -g serve

COPY --from=builder /app/build ./build

# Expose port
EXPOSE 3000

# Health check - Just check if server is running
HEALTHCHECK --interval=15s --timeout=10s --start-period=10s --retries=5 \
    CMD node -e "require('http').get('http://localhost:3000', (r) => {if (r.statusCode !== 404) throw new Error(r.statusCode)})"

# Start the app
CMD ["serve", "-s", "build", "-l", "3000"]

