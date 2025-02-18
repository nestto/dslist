# DSList

Bem-vindo ao DSList! Este é um projeto de demonstração para a criação de uma lista de jogos utilizando Spring Boot.

## Sobre o Projeto

O DSList é uma aplicação que permite gerenciar listas de jogos. Você pode adicionar, remover e listar jogos, além de organizar os jogos em diferentes listas.

## Estrutura do Projeto

A estrutura do projeto é a seguinte:


## Configuração do Ambiente

### Usando H2

1. Configure o banco de dados H2 conforme as propriedades presentes em [`src/main/resources/application-test.properties`](src/main/resources/application-test.properties).

### Usando PostgreSQL com Docker

1. Configure as propriedades de acesso ao PostgreSQL conforme em [`application-test.properties`](src/main/resources/application-test.properties).
2. Utilize o arquivo [`docker-compose.yml`](docker-compose.yml) com o seguinte conteúdo:
3. Inicie o container com Docker Compose:
    ```sh
    docker-compose up -d
    ```

## APIs Disponíveis

### Listar todas as listas de jogos

- **Endpoint:** `/lists`
- **Método:** `GET`
- **Resposta:**
    ```json
    [
        {
            "id": 1,
            "name": "Aventura e RPG"
        },
        {
            "id": 2,
            "name": "Jogos de plataforma"
        }
    ]
    ```

### Listar jogos por lista

- **Endpoint:** `/lists/{listid}/games`
- **Método:** `GET`
- **Parâmetros:**
    - `listid`: ID da lista de jogos
- **Resposta:**
    ```json
    [
        {
            "id": 1,
            "title": "Mass Effect Trilogy",
            "year": 2012,
            "imgUrl": "https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/1.png",
            "shortDescription": "Lorem ipsum dolor sit amet consectetur adipisicing elit."
        },
        ...
    ]
    ```

### Mover jogo na lista

- **Endpoint:** `/lists/{listid}/replacement`
- **Método:** `POST`
- **Parâmetros:**
    - `listid`: ID da lista de jogos
- **Corpo da Requisição:**
    ```json
    {
        "sourceIndex": 0,
        "destinationIndex": 1
    }
    ```
- **Exemplo de Resposta (ordem dos jogos trocada):**
    ```json
    [
        {
            "id": 2,
            "title": "The Witcher 3: Wild Hunt",
            "year": 2015,
            "imgUrl": "https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/2.png",
            "shortDescription": "Lorem ipsum dolor sit amet consectetur adipisicing elit."
        },
        {
            "id": 1,
            "title": "Mass Effect Trilogy",
            "year": 2012,
            "imgUrl": "https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/1.png",
            "shortDescription": "Lorem ipsum dolor sit amet consectetur adipisicing elit."
        }
    ]
    ```

## Testando a API com Postman

Você pode utilizar o Postman para realizar testes de requisições GET e POST.

### GET – Listar todas as listas de jogos

- **Endpoint:** `/lists`
- **Método:** `GET`

Exemplo de requisição no Postman:
1. Abra o Postman.
2. Crie uma nova requisição com método GET.
3. Informe a URL: `http://localhost:8080/lists`
4. Envie a requisição e veja a resposta, que deverá ser semelhante a:
    ```json
    [
        {
            "id": 1,
            "name": "Aventura e RPG"
        },
        {
            "id": 2,
            "name": "Jogos de plataforma"
        }
    ]
    ```

### POST – Mover jogo na lista

- **Endpoint:** `/lists/{listid}/replacement`
- **Método:** `POST`
- **Parâmetros:**
  - `listid`: ID da lista de jogos (incluso na URL)
- **Corpo da Requisição (JSON):**
    ```json
    {
        "sourceIndex": 0,
        "destinationIndex": 1
    }
    ```

Exemplo de requisição no Postman:
1. Abra o Postman.
2. Crie uma nova requisição com método POST.
3. Informe a URL, substituindo `{listid}` pelo ID desejado:
   `http://localhost:8080/lists/1/replacement`
4. Na aba "Body", selecione a opção "raw" e escolha o tipo JSON.
5. Insira o JSON do exemplo acima e envie a requisição.
6. A resposta deverá indicar a nova ordem dos jogos, por exemplo:
    ```json
    [
        {
            "id": 2,
            "title": "The Witcher 3: Wild Hunt",
            "year": 2015,
            "imgUrl": "https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/2.png",
            "shortDescription": "Lorem ipsum dolor sit amet consectetur adipisicing elit."
        },
        {
            "id": 1,
            "title": "Mass Effect Trilogy",
            "year": 2012,
            "imgUrl": "https://raw.githubusercontent.com/devsuperior/java-spring-dslist/main/resources/1.png",
            "shortDescription": "Lorem ipsum dolor sit amet consectetur adipisicing elit."
        }
    ]
    ```
