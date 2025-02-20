# Étape 1 : Utiliser une image officielle de Node.js
FROM node:22.12.0-alpine

RUN apk add --no-cache python3 make g++ openssl

# Étape 2 : Définir le répertoire de travail
WORKDIR /app

# Étape 3 : Copier les fichiers du projet
COPY package.json ./

# Étape 4 : Installer les dépendances
RUN npm install
RUN npm rebuild bcrypt --build-from-source

# Étape 5 : Copier le reste des fichiers
COPY . .

# Étape 6 : Générer le client Prisma
RUN npx prisma generate

# Étape 7 : Exposer le port
EXPOSE 3000

# Étape 8 : Démarrer l'application
CMD ["node", "server.js"]
