# Usa una imagen de Maven como base
FROM maven:3.8.4-openjdk-11 AS build

# Copia el código fuente al contenedor
COPY ./ /usr/src/app

# Establece el directorio de trabajo
WORKDIR /usr/src/app

# Empaqueta la aplicación usando Maven
RUN mvn clean install

# Segunda etapa para la imagen de producción
FROM openjdk:11-jre-slim

# Establece el directorio de trabajo en /app
WORKDIR /app

# Copia el archivo JAR de la etapa de construcción al contenedor
COPY --from=build /usr/src/app/target/employeemanager-*.jar app.jar

# Expone el puerto 8080
EXPOSE 8080

# Comando para ejecutar la aplicación cuando el contenedor se inicia
CMD ["java", "-jar", "app.jar"]