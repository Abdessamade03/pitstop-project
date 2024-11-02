# Stage de build
FROM node:20.13-alpine as builder

WORKDIR /usr/src/app

# Mise à jour de la liste des paquets et mise à niveau de tous les paquets pour réduire les vulnérabilités
RUN apk update && apk upgrade && \
    apk add --no-cache build-base

# Copier les fichiers de dépendance
COPY package*.json ./
# Mettre à jour les dépendances et installer les autres dépendances
RUN npm install --production && npm update
RUN npm ci --only=production

# Copier le reste de l'application
COPY . .

# Créer et configurer un utilisateur non privilégié
RUN adduser -D appuser && chown -R appuser:appuser /usr/src/app

# Stage final
FROM node:20.13-alpine
# Définir l'environnement de production
ENV NODE_ENV=production

WORKDIR /usr/src/app

# Créer l'utilisateur et configurer les permissions avant de copier les fichiers
RUN adduser -D appuser && mkdir -p /home/appuser/.npm && chown -R appuser:appuser /home/appuser

# Copier depuis le builder
COPY --from=builder /usr/src/app /usr/src/app
COPY --from=builder /etc/passwd /etc/passwd

# Assurer que tous les fichiers et répertoires nécessaires appartiennent à l'utilisateur non privilégié
RUN chown -R appuser:appuser /usr/src/app

USER appuser

EXPOSE 8080

# Démarrer le serveur Express Gateway
CMD ["node", "server.js"]
