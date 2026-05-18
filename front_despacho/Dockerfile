
#--- ETAPA 1: Construcción del Frontend ---
FROM node:18-alpine AS build-stage
WORKDIR /app
# Copiamos los archivos de dependencias de Node
COPY package*.json ./
# Instalamos las librerías de React
RUN npm install
# Copiamos todo el código del Front
COPY . .
# Compilamos la aplicación (Vite creará una carpeta llamada 'dist')
RUN npm run build




#--- ETAPA 2: Servidor de Producción ---
FROM nginx:1.25-alpine
WORKDIR /usr/share/nginx/html
# Eliminamos los archivos por defecto que trae Nginx
RUN rm -rf ./*
# Copiamos los archivos compilados en la Etapa 1 hacia el servidor Nginx
COPY --from=build-stage /app/dist .
# Exponemos el puerto estándar para páginas web
EXPOSE 80
# Encendemos Nginx
CMD ["nginx", "-g", "daemon off;"]


