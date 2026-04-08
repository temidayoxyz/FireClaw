FROM node:20-slim
RUN apt-get update && apt-get install -y curl git && rm -rf /var/lib/apt/lists/*
WORKDIR /app
COPY package*.json ./
RUN npm install --production
COPY . .
ENV NODE_ENV=production
RUN mkdir -p /app/data
ENV OPENCLAW_STATE_DIR=/app/data
EXPOSE 8080
CMD ["npm", "start"]