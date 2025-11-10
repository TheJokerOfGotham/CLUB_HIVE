# Use lightweight Node.js image
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Copy backend package files
COPY club-hive/backend/package*.json ./

# Install only production dependencies
RUN npm install --omit=dev

# Copy all backend source code
COPY club-hive/backend .

# Set environment to production
ENV NODE_ENV=production

# Expose backend port
EXPOSE 5000

# Start the server
CMD ["node", "server.js"]

