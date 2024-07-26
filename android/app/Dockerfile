# Use the official Flutter image
FROM cirrusci/flutter:stable

# Set the working directory
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . .

# Get dependencies
RUN flutter pub get

# Build the Flutter web application
RUN flutter build web

# Use nginx to serve the Flutter web application
FROM nginx:alpine
COPY --from=0 /app/build/web /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx server
CMD ["nginx", "-g", "daemon off;"]
