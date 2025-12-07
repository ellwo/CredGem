# Use Node.js as the base image
FROM node:18-alpine

# Set working directory
WORKDIR /app

# Copy package files first
COPY package*.json ./

# Install dependencies
RUN npm cache clean --force && \
    npm install --legacy-peer-deps

# Copy the rest of the application
COPY . .

ARG VITE_API_URL
ENV VITE_API_URL $VITE_API_URL

# Build the application for production
RUN npm run build

# Create entrypoint script to copy built files to volume
RUN echo '#!/bin/sh' > /entrypoint.sh && \
    echo 'echo "Copying built files to volume..."' >> /entrypoint.sh && \
    echo 'cp -r /app/dist/* /app/static/ || true' >> /entrypoint.sh && \
    echo 'echo "Files copied. Keeping container alive..."' >> /entrypoint.sh && \
    echo 'while true; do sleep 3600; done' >> /entrypoint.sh && \
    chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
