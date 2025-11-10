# --- Build stage ---
FROM node:20-alpine AS build
WORKDIR /app

# Copy package files and install deps
COPY package*.json ./
RUN npm install

# Copy everything else
COPY . .

# 👇 Inject Render environment variable at build time
ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL}

# Build the frontend
RUN npm run build

# --- Serve stage ---
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

