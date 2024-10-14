# Etapa 1: Build da aplicação
FROM maven:latest AS build
WORKDIR /app

# Copia o arquivo pom.xml e baixa as dependências do projeto
COPY pom.xml .
RUN mvn dependency:go-offline

# Copia todo o código fonte do projeto e faz o build
COPY src ./src
RUN mvn clean package -DskipTests

# Etapa 2: Imagem final da aplicação
FROM eclipse-temurin:21-jdk-alpine
WORKDIR /app

# Copia o jar gerado na etapa de build
COPY --from=build /app/target/helloworld-0.0.1-SNAPSHOT.jar app.jar

# Define o comando de execução da aplicação
ENTRYPOINT ["java", "-jar", "app.jar"]
