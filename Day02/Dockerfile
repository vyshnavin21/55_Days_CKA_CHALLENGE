# Use Node.js 18 on Alpine Linux as the base image (lightweight OS)
FROM node:18-alpine

# Set the working directory inside the container.
# All subsequent commands (RUN, COPY, CMD) will run from /app.
WORKDIR /app

# Copy package.json and package-lock.json first.
# This is a caching optimization — npm install only re-runs
# when these files change, not on every source code change.
COPY package*.json ./

# Install dependencies during image build time
RUN npm install

# Copy all remaining source files from local machine to /app in the container
COPY . .

# Documents that the app listens on port 3000.
# Note: this does NOT publish the port — use -p 3000:3000 in docker run.
EXPOSE 3000

# Command to run when the container starts (starts the Node.js server)
CMD ["npm", "start"]
