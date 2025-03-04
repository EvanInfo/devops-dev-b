# Étape 1 : Utiliser une image officielle de Node.js
FROM node:22.12.0-alpine

RUN apk add --no-cache python3 make g++ openssl

# Étape 2 : Définir le répertoire de travail
WORKDIR /app

# Étape 3 : Copier uniquement package.json
COPY package.json ./

# 🔥 Générer package-lock.json s'il n'existe pas
RUN npm install --package-lock-only

# Étape 4 : Copier package-lock.json après sa génération
COPY package-lock.json ./

# Étape 5 : Installer les dépendances en mode production (optimisation du cache)
RUN npm ci --only=production

RUN npm rebuild bcrypt --build-from-source

# Étape 6 : Copier le reste des fichiers
COPY . .

# Étape 7 : Générer le client Prisma
RUN npx prisma generate
RUN npx prisma db push
RUN npx prisma db seed

# Étape 8 : Exposer le port
EXPOSE 3000

# Étape 9 : Démarrer l'application
CMD ["node", "server.js"]
