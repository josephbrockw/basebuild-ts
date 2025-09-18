FROM node:20-alpine

WORKDIR /app

# Install dependencies
COPY package.json ./
RUN npm install

# Copy source code
COPY . .

# Build the app
RUN npm run build

EXPOSE 3001

CMD ["npm", "run", "start:dev"]
