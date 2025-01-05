# Step 1: Use the official Node.js image as the base image
FROM node:18-alpine AS build

# Step 2: Set the working directory inside the container
WORKDIR /app

# Step 3: Copy package.json and package-lock.json (or yarn.lock) to the working directory
COPY package*.json ./

# Step 4: Install dependencies
RUN npm install

# Step 5: Copy the rest of the application code
COPY . .

# Step 6: Build the Vite application
RUN npm run build

# Step 7: Use the official Nginx image for serving the built files
FROM nginx:stable-alpine

# Step 8: Copy the build output from the previous stage to the Nginx web directory
COPY --from=build /app/dist /usr/share/nginx/html

# Step 9: Expose port 80 for the application
EXPOSE 80

# Step 10: Start Nginx when the container launches
CMD ["nginx", "-g", "daemon off;"]
