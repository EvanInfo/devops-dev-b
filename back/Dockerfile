# Étape 1 : Utiliser une image officielle de Node.js
FROM node:22.12.0-alpine

# Étape 2 : Installer les outils nécessaires
RUN apk add --no-cache python3 make g++ openssl

# Étape 3 : Définir le répertoire de travail
WORKDIR /app

# Étape 4 : Copier uniquement package.json
COPY package.json ./

# 🔥 Étape 5 : Installer les dépendances et générer package-lock.json
RUN npm install

# Étape 6 : Copier tout le reste du projet
COPY . .

# Étape 7 : Générer le client Prisma et préparer la DB
RUN npx prisma generate
RUN npx prisma db push
RUN npx prisma db seed

# Étape 8 : Exposer le port
EXPOSE 3000

# Étape 9 : Démarrer l'application
CMD ["node", "server.js"]
