FROM nginx:alpine

# Remove default nginx static assets
RUN rm -rf /usr/share/nginx/html/*

# Copy static assets into nginx
COPY html /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Add a health check to monitor container health
HEALTHCHECK --interval=30s --timeout=3s \
  CMD wget -qO- http://localhost/ || exit 1

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
