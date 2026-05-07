# ==========================================
# Etapa 1: Construcción (Builder)
# ==========================================
FROM node:18-alpine AS builder
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# ==========================================
# Etapa 2: Ejecución (Runner)
# ==========================================
FROM nginxinc/nginx-unprivileged:alpine
COPY --from=builder /app/dist /usr/share/nginx/html

# Aquí inyectamos el proxy secreto para conectar con el backend privado
COPY nginx.conf /etc/nginx/conf.d/default.conf 

EXPOSE 8080
CMD ["nginx", "-g", "daemon off;"]