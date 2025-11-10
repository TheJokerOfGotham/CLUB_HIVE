# --- Build stage ---
FROM node:20-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# --- Serve stage ---
FROM nginx:alpine

# Copy React build files
COPY --from=build /app/dist /usr/share/nginx/html

# Remove the default Nginx config
RUN rm /etc/nginx/conf.d/default.conf

# Add our custom config for React Router
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

