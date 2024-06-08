# Use the official Nginx image from Docker Hub
FROM nginx:latest

# Copy custom configuration file from the current directory to the container
#COPY nginx.conf /etc/nginx/nginx.conf
COPY conf.d/nginx_reverse.conf /etc/nginx/conf.d/default.conf

# Copy website content to the container
COPY html /usr/share/nginx/html

# Expose port 80
EXPOSE 8080