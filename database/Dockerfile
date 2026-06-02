# Image de base officielle PostgreSQL légère
FROM postgres:17.2-alpine

# Définition des variables d'environnement par défaut pour la base de données
ENV POSTGRES_DB=db \
    POSTGRES_USER=usr \
    POSTGRES_PASSWORD=pwd

# Copie automatique des scripts SQL d'initialisation (schéma et données)
COPY 01-CreateScheme.sql /docker-entrypoint-initdb.d/
COPY 02-InsertData.sql /docker-entrypoint-initdb.d/