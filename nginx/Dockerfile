FROM nginx:1.25-alpine

# Install wget for healthcheck
RUN apk add --no-cache wget

# Copy custom nginx configuration
COPY nginx.conf /etc/nginx/nginx.conf

