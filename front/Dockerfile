# Étape 1 : Build du frontend avec Node.js
FROM node:22.12.0-alpine AS build

WORKDIR /app

# Étape 2 : Copier uniquement package.json
COPY package.json ./

# 🔥 Étape 3 : Installer les dépendances et générer package-lock.json
RUN npm install

# Étape 4 : Copier le reste des fichiers
COPY . .

# Étape 5 : Passer la variable d'environnement au build
ARG VITE_API_URL
ENV VITE_API_URL=${VITE_API_URL}

RUN echo "🚀 VITE_API_URL au build : $VITE_API_URL"
RUN npm run build

# Étape 6 : Utiliser Nginx pour servir les fichiers statiques
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html

# 🔥 Assurer que la variable VITE_API_URL est définie dans l'environnement du container final
ENV VITE_API_URL=${VITE_API_URL}

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
