# --- Build stage ---
FROM node:20-alpine AS build
WORKDIR /app

# Copy frontend package files and install
COPY club-hive/frontend/package*.json ./
RUN npm install

# Copy frontend source and build (Vite will read import.meta.env.VITE_API_URL)
COPY club-hive/frontend .
ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL:-http://localhost:5001}
RUN npm run build

# --- Serve stage ---
FROM nginx:alpine
# Add custom nginx config for SPA fallback
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy built assets
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80 for Render
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]

