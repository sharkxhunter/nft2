# ==== CONFIGURE FOR DEVELOPMENT =====
FROM node:16.18-alpine AS development

# Set working directory
WORKDIR client

# Cache and Install dependencies
COPY package.json .
COPY package-lock.json .

# Install dependencies (npm ci makes sure the exact versions in the lockfile gets installed)
RUN npm ci

# Copy client files
COPY . .

# ==== BUILD AND TEST =====
# Test the app
RUN CI=true npm run test

# Build the app
RUN CI=true npm run build

# ==== RUN =======

# Expose the port on which the app will be running (50666 is the default that `serve` uses)
EXPOSE 50666:50666

# Start the app
CMD [ "npx", "serve", "build" ]

# Build the Docker image for the current folder and tag it with `fxethers-client-development`, file `Dockerfile.development`
# docker build -t fxethers-client-development -f Dockerfile.development .

# Check the image was created
# docker images | grep fxethers-client-development

# Run the image in detached mode and map port 50666 inside the container with 50666 on current host
# docker run -p 50666:50666 -d fxethers-client-development