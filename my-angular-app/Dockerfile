# Step 1: Build the Angular app
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package.json & package-lock.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the app and build it
COPY . .
RUN npm run build --prod

# Step 2: Serve the app with Nginx
FROM nginx:stable-alpine

# Copy the build output from the builder stage to Nginx public folder
COPY --from=builder /app/dist/ /usr/share/nginx/html


# Expose port 80
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
