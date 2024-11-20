# Étape de construction
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
RUN npm install -g @angular/cli
COPY . .
RUN npm run build --configuration=production

# Étape de serveur
FROM nginx:alpine
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/dist/app/browser /usr/share/nginx/html
EXPOSE 80
#CMD ["nginx", "-g", "daemon off;"]
