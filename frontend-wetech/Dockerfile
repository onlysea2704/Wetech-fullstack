# Stage 1: Build React app
FROM node:20-alpine AS build
WORKDIR /app

# Nhận biến REACT_APP_BACKEND_URL từ Docker Compose
ARG REACT_APP_BACKEND_URL
# Thiết lập biến môi trường cho quá trình build
ENV REACT_APP_BACKEND_URL=${REACT_APP_BACKEND_URL}

COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
