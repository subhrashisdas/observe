# Use the official Node.js image
FROM node:14

# Set the working directory
WORKDIR /usr/src/app

# Copy package.json (not strictly necessary if there are no dependencies)
COPY package*.json ./

# Install dependencies (not necessary, but included for completeness)
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose the application port
EXPOSE 8000

# Command to run the application
CMD ["node", "index.js"]
