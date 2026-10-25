#Base IMage

FROM node:22-alpine AS builder

#Working Direcotry
WORKDIR /app

#COPY source code to container working directory
COPY . .

#INstalling dependencies
RUN npm install

#Building the app
RUN npm run build

#Using the Slim image to run ---------------------------------
FROM node:22-slim

#Working Directory
WORKDIR /app

COPY --from=builder /app/node_modules ./node_modules
COPY --from=builder /app/dist ./dist

CMD ["npm", "start"]
