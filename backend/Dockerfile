# 1. Étape de Build (JDK)
FROM eclipse-temurin:21-jdk-alpine AS myapp-build
ENV MYAPP_HOME=/opt/myapp
WORKDIR $MYAPP_HOME

RUN apk add --no-cache maven

# Optimisation du cache pour sauvegarder les dépendances Maven
COPY pom.xml .
RUN mvn dependency:go-offline

# Copie des sources et packaging
COPY src ./src
RUN mvn package -DskipTests

# 2. Étape d'Exécution (JRE - beaucoup plus légère)
FROM eclipse-temurin:21-jre-alpine
ENV MYAPP_HOME=/opt/myapp
WORKDIR $MYAPP_HOME

# Récupération uniquement du fichier JAR généré à l'étape précédente
COPY --from=myapp-build $MYAPP_HOME/target/*.jar $MYAPP_HOME/myapp.jar

EXPOSE 8080
ENTRYPOINT ["java", "-jar", "myapp.jar"]