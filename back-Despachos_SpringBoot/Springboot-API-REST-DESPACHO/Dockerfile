# --- ETAPA 1: Compilación ---
FROM maven:3.8.5-openjdk-17 AS builder
WORKDIR /app
# Copiamos la lista de dependencias y el código fuente
COPY pom.xml .
COPY src ./src
# Compilamos el proyecto y generamos el archivo ejecutable .jar
RUN mvn clean package -DskipTests

# --- ETAPA 2: Ejecución  ---
FROM eclipse-temurin:17-jdk
WORKDIR /app

# PRÁCTICA DE SEGURIDAD: Creamos un usuario no-root (Mínimo privilegio)
RUN useradd -m devopsuser

# Copiamos solo el ejecutable que se fabricó en la Etapa 1
COPY --from=builder /app/target/*.jar app.jar

# Cambiamos al usuario seguro
USER devopsuser

# Exponemos el puerto estándar de Spring Boot
EXPOSE 8080

# Comando para encender el backend
ENTRYPOINT ["java", "-jar", "app.jar"]