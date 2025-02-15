# Use a imagem oficial do Nginx com menor tamanho
FROM nginx:alpine

# Defina o diretório de trabalho
WORKDIR /app

# Copie o arquivo index.html para o diretório de trabalho
COPY index.html /app

# Defina a variável de ambiente
ENV APP_VERSION=1.0.0

# Instale curl, htop e wget
RUN apk update && apk add --no-cache curl htop wget

# Configure o Nginx para servir o conteúdo do /app
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Exponha a porta 80
EXPOSE 80

# Inicie o serviço do Nginx
CMD ["nginx", "-g", "daemon off;"]
