# Étape 1 : Utiliser une image Node.js pour la build
FROM node:22.12.0

# Étape 2 : Définir le répertoire de travail
WORKDIR /app

# Étape 3 : Copier les fichiers package.json et package-lock.json
COPY package.json package-lock.json ./

# Étape 4 : Installer les dépendances
RUN npm install

# Étape 5 : Copier le reste des fichiers après l’installation des dépendances
COPY . .

# Étape 6 : Construire l’application avec Vite
RUN npm run build


FROM httpd:alpine

# Copier les fichiers buildés dans le dossier Apache
COPY --from=builder /app/dist/ /usr/local/apache2/htdocs/

# Exposer le port 80
EXPOSE 80

# Démarrer Apache
CMD ["httpd", "-D", "FOREGROUND"]