# desafio-modulo-docker-stackx
Este repositório contém as atividades do desafio do módulo Docker da StackX. As atividades são divididas em duas partes: empacotamento de uma aplicação simples de frontend utilizando nginx e implementação da plataforma de documentação Wiki.js.

# Estrutura do Repositório
atv1/: Empacotamento de uma aplicação simples de frontend.

atv2/: Implementação da plataforma de documentação Wiki.js.

# Atividades
Atividade 1: Empacotamento de Aplicação Frontend
Nesta atividade, empacotamos uma aplicação simples de frontend composta por um único arquivo index.html. A aplicação é empacotada utilizando a imagem oficial do nginx como base, com alguns requisitos específicos.

Atividade 2: Implementação da Plataforma Wiki.js
Nesta atividade, implementamos a plataforma de documentação Wiki.js com um banco de dados Postgres para a persistência de dados. Um container é responsável pelo banco de dados e outro pela aplicação Wiki.js.

# Tecnologias Utilizadas
Docker

Nginx

Wiki.js

PostgreSQL

# README da Atividade 1
Atividade 1: Empacotamento de Aplicação Frontend
# Descrição
Esta atividade envolve empacotar uma aplicação simples de frontend composta por um arquivo index.html. Utilizamos a imagem oficial do nginx como base e seguimos alguns requisitos específicos para configurar o container.

# Requisitos
Utilize a imagem oficial do nginx com menor tamanho (nginx:alpine).

Defina o diretório de trabalho dentro do container como /app.

Copie o arquivo index.html para o diretório de trabalho definido.

Utilize a variável de ambiente APP_VERSION com o valor 1.0.0.

Garanta que o serviço do nginx execute assim que o container seja iniciado.

A porta de comunicação na rede deverá ser TCP/80.

Instale os aplicativos curl, htop e wget na imagem.

Dockerfile
dockerfile
FROM nginx:alpine
WORKDIR /app
COPY index.html /app
ENV APP_VERSION=1.0.0
RUN apk add --no-cache curl htop wget
CMD ["nginx", "-g", "daemon off;"]
EXPOSE 80
Como Iniciar
Navegue até o diretório atv1.

Construa a imagem Docker:


docker build -t meu-nginx .
Inicie o container:


docker run -d -p 80:80 meu-nginx

# README da Atividade 2
Atividade 2: Implementação da Plataforma Wiki.js
# Descrição
O objetivo desta atividade é implementar a plataforma de documentação Wiki.js, utilizando um container de banco de dados Postgres para a persistência de dados e outro container para a aplicação Wiki.js.

# Requisitos
Configure um container para o banco de dados Postgres.

Configure um container para a aplicação Wiki.js.

Navegue pela documentação oficial do Wiki.jspara obter as especificações necessárias.

Garanta que os serviços sejam corretamente configurados e estejam prontos para uso.

docker-compose.yml

version: '3'
services:
  postgres:
    image: postgres:13-alpine
    environment:
      POSTGRES_DB: wikidb
      POSTGRES_USER: wikiuser
      POSTGRES_PASSWORD: wikipassword
    volumes:
      - postgres_data:/var/lib/postgresql/data

  wikijs:
    image: requarks/wiki:2
    environment:
      DB_TYPE: postgres
      DB_HOST: postgres
      DB_PORT: 5432
      DB_USER: wikiuser
      DB_PASS: wikipassword
      DB_NAME: wikidb
    depends_on:
      - postgres
    ports:
      - "3000:3000"

volumes:
  postgres_data:
Como Iniciar
Navegue até o diretório atv2.

# Inicie os containers com Docker Compose:


docker-compose up -d
Cadastro no Wiki.js
Para utilizar a plataforma Wiki.js, você precisará criar uma conta. Acesse a aplicação no navegador (http://localhost:3000) e siga as instruções para realizar o cadastro.
