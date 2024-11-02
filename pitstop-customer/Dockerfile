# Stage de build
FROM node

WORKDIR /app

# Update package list and upgrade all packages to reduce vulnerabilities
# RUN apk update && apk upgrade && \
#     apk add --no-cache build-base
# Installer les packages nécessaires pour la compilation
#RUN apk add --no-cache build-base
# Copier les fichiers de dépendance
COPY package*.json ./
# Mettre à jour la dépendance minimist à une version sécurisée
RUN npm install
# Installer les autres dépendances
# RUN npm ci --only=production
  
# Copier le reste de l'application
COPY . .

# Créer et configurer un utilisateur non privilégié
# RUN adduser -D appuser && chown -R appuser:appuser /app

# # Stage final
# FROM node
# # Définir l'environnement de production
ENV NODE_ENV=production

# WORKDIR /app

# # Créer l'utilisateur et configurer les permissions avant de copier les fichiers
# # RUN adduser -D appuser && mkdir -p /home/appuser/.npm && chown -R appuser:appuser /home/appuser

# # RUN npm install -g npm@10.8.0 && \
# #     npm install sequelize-cli@6.6.2

# RUN npm install
# # Copier depuis le builder
# COPY --from=builder /app /app
# # COPY --from=builder /etc/passwd /etc/passwd

# # Assurer que tous les fichiers et répertoires nécessaires appartiennent à l'utilisateur non privilégié
# # RUN chown -R appuser:appuser /app

# # USER appuser

EXPOSE 3001
CMD ["npm", "start"]
