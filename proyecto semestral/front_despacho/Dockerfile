# 1.- Builder 
FROM maven:3.9-eclipse-temurin-17-alpine AS builder
WORKDIR /app

# Copiamos dependencias para cache
COPY package*.json ./
# Instalamos dependencias
RUN npm install
# Copiamos codigo Fuente
COPY . .
RUN npm run build

# ==============================
# 2.- Runner

#Usamos una imagen de Nginx unprivileged 
FROM nginxinc/nginx-unprivileged:alpine 

# Copiamos los archivos de construcción al directorio de Nginx
COPY --from=builder /app/dist /usr/share/nginx/html

# Aquí inyectamos el proxy secreto para conectar con el backend privado
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Exponemos el puerto
EXPOSE 8080

# Comando para ejecutar Nginx
CMD ["nginx", "-g", "daemon off;"]

