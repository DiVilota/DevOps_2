# 1.- Builder 

FROM maven:3.9-eclipse-temurin-17-alpine AS builder
WORKDIR /app

# Copiamos el Pom para el cache
COPY pom.xml .
# Descargamos dependencias

#Copiamos codigo Fuente
COPY src ./src
RUN mvn clean package -DskipTests

# ==============================

# 2.- Runner
FROM eclipse-temurin:17-alpine
WORKDIR /app

#Crear User y Grupo no root
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser:appgroup

# Copiamos el JAR generado
COPY --from=builder /app/target/*.jar app.jar

# Exponemos el puerto
EXPOSE 8080

# Comando para ejecutar la aplicación
ENTRYPOINT ["java", "-jar", "app.jar"]
