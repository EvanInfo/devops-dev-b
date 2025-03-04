# Étape 1 : Build du frontend avec Node.js
FROM node:22.12.0-alpine AS build

WORKDIR /app

# Étape 2 : Copier uniquement package.json
COPY package.json ./

# 🔥 Générer package-lock.json si absent
RUN npm install --package-lock-only

# Étape 3 : Copier package-lock.json après sa génération
COPY package-lock.json ./

# Étape 4 : Installer les dépendances
RUN npm ci --only=production

# Étape 5 : Copier le reste des fichiers
COPY . .

# Étape 6 : Définir l'URL de l'API au build
ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL}

RUN echo "🚀 VITE_API_URL au build : $VITE_API_URL"  # Debugging

# Étape 7 : Construire le frontend
RUN npm run build

# Étape 8 : Utiliser Nginx pour servir le frontend
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
