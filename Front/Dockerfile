# Usa la imagen de Node.js para la construcción
FROM node:20-alpine AS build

# Establece el directorio de trabajo
WORKDIR /Front

# Copia los archivos de package y package-lock
COPY package*.json ./

# Instala las dependencias
RUN npm install

# Copia el resto del código de la aplicación
COPY . .

# Construye la aplicación Angular
RUN npm run build --prod

# Usa una imagen de Nginx para servir la aplicación
FROM nginx:alpine

# Copia los archivos construidos al directorio de Nginx
COPY --from=build /app/dist/Front /usr/share/nginx/html

# Expone el puerto 4100
EXPOSE 80

# Inicia Nginx
CMD ["nginx", "-g", "daemon off;"]
