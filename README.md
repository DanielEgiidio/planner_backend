<h1 align="center">
  Plann.er
</h1>

<p align="center">
  <img alt="GitHub language count" src="https://img.shields.io/github/languages/count/danielegiidio/planner_backend">

  <img alt="GitHub Top Language" src="https://img.shields.io/github/languages/top/danielegiidio/planner_backend" />

  <img alt="Repository size" src="https://img.shields.io/github/repo-size/danielegiidio/planner_backend">
  
  <a href="https://github.com/pabloxt14/nlw-journey-node/commits/master">
    <img alt="GitHub last commit" src="https://img.shields.io/github/last-commit/danielegiidio/planner_backend">
  </a>
    
   <img alt="License" src="https://img.shields.io/badge/license-MIT-blue">


</p>

<p align="center" >
  <img src="https://i.ibb.co/tQnnLFD/Cover.png" alt="Capa do projeto"  />
</p>



<p align="center">
 <a href="#-about">About</a> | 
 <a href="#-routes">Routes</a> | 
 <a href="#-setup">Setup</a> | 
 <a href="#-technologies">Technologies</a> | 
 <a href="#-license">License</a>
</p>


## 💻 About

Plann.er é uma aplicação de planejamento de viagens que permite criar e gerenciar planos de viagem de forma colaborativa. Com Plann.er, você pode:

- Montar planos de viagens com amigos.
- Registrar atividades e eventos importantes.
- Adicionar links úteis e recursos sobre a viagem.

<!-- ## 🔗 Deploy

O deploy da aplicação pode ser acessada através da seguinte URL base: https://pabloxt14-nlw-expert-notes.vercel.app/ -->


## ⛕ Routes

### Trips Routes

#### POST `/trips`

Cria uma nova viagem.

##### Request body

```json
{
    "destination": "Florianóplis",
    "starts_at": "2024-08-10 10:00:00",
    "ends_at": "2024-08-20 10:00:00",
    "owner_name": "Daniel Egidio",
    "owner_email": "daniel@gmail.com",
    "emails_to_invite": [
        "daniel@gmail.com",
        "johndoe@gmail.com"
    ]
}
```

##### Response body

```json
{
    "tripId": "ce32c8a5-2c13-44fd-8050-27dfcf24c201"
}
```

#### GET `/trips/:tripId`

Retorna os detalhes de uma viagem.

##### Response body

```json
{
    "trip": {
        "id": "ce32c8a5-2c13-44fd-8050-27dfcf24c201",
        "destination": "Florianóplis",
        "starts_at": "2024-08-10T13:00:00.000Z",
        "ends_at": "2024-08-20T13:00:00.000Z",
        "is_confirmed": false
    }
}
```

#### PUT `/trips/:tripId`

Altera uma viagem.

##### Request body

```json
{
    "destination": "Florianóplis - SC",
    "starts_at": "2024-08-15 10:00:00",
    "ends_at": "2024-08-20 10:00:00"
}
```

##### Response body

```json
{
    "tripId": "ce32c8a5-2c13-44fd-8050-27dfcf24c201"
}
```



#### GET `/trips/:tripId/confirm`

Confirma uma viagem.

### Participants Routes

#### POST `/trips/:tripId/invites`

Envia um convite a um participante para uma viagem.

##### Request body

```json
{
    "email": "teste@gmail.com"
}
```

##### Response body

```json
{
    "participantId": "7a008aa3-134b-4e72-a531-7ebb41010c7b"
}
```

#### GET `/trips/:tripId/participants`

Retorna os participantes de uma viagem.

##### Response body

```json
{
    "participants": [
        {
            "id": "4693de37-1d8c-492a-9025-53cae2300f24",
            "name": "Daniel Egidio",
            "email": "daniel@gmail.com",
            "is_confirmed": true
        },
        {
            "id": "59ce11ac-50ef-4739-b444-458156bce2a7",
            "name": null,
            "email": "johndoe@gmail.com",
            "is_confirmed": false
        },
        {
            "id": "7a008aa3-134b-4e72-a531-7ebb41010c7b",
            "name": null,
            "email": "teste@gmail.com",
            "is_confirmed": false
        }
    ]
}
```

#### GET `/participants/:participantId`

Retorna os detalhes de um participante.

##### Response body

```json
{
    "participant": {
        "id": "7a008aa3-134b-4e72-a531-7ebb41010c7b",
        "name": null,
        "email": "teste@gmail.com",
        "is_confirmed": false
    }
}
```

#### GET `/participants/:participantId/confirm`

Confirma um participante na viagem.

### Activities Routes

#### POST `/trips/:tripId/activities`

Cria uma atividade em uma viagem.

##### Request body

```json
{
  "title": "Academia",
  "occurs_at": "2024-08-18 18:00:00"
}
```

##### Response body

```json
{
  "activityId": "f944daf7-e7e6-47a2-b050-1556d6a9e963"
}
```

#### GET `/trips/:tripId/activities`

Retorna as atividades de uma viagem.

##### Response body

```json
{
    "activities": [
        {
            "date": "2024-08-15T13:00:00.000Z",
            "activities": []
        },
        {
            "date": "2024-08-16T13:00:00.000Z",
            "activities": []
        },
        {
            "date": "2024-08-17T13:00:00.000Z",
            "activities": []
        },
        {
            "date": "2024-08-18T13:00:00.000Z",
            "activities": [
                {
                    "id": "d63bcbbc-3c50-4cb6-8961-c1f9c6e5fabf",
                    "title": "Academia",
                    "occurs_at": "2024-08-18T21:00:00.000Z",
                    "trip_id": "ce32c8a5-2c13-44fd-8050-27dfcf24c201"
                }
            ]
        },
        {
            "date": "2024-08-19T13:00:00.000Z",
            "activities": []
        },
        {
            "date": "2024-08-20T13:00:00.000Z",
            "activities": []
        }
    ]
}
```

### Links Routes

#### POST `/trips/:tripId/links`

Cria um link em uma viagem.

##### Request body

```json
{
    "title" : "Reserva do AirBnB",
    "url" : "http://airbnb.com/reserva-journey"
}
```

##### Response body

```json
{
    "linkId": "e1b00fc4-f99a-4cd5-b33a-6db2b3b72716"
}
```

#### GET `/trips/:tripId/links`

Retorna os links de uma viagem.

##### Response body

```json
{
    "links": [
        {
            "id": "e1b00fc4-f99a-4cd5-b33a-6db2b3b72716",
            "title": "Reserva do AirBnB",
            "url": "http://airbnb.com/reserva-journey",
            "trip_id": "ce32c8a5-2c13-44fd-8050-27dfcf24c201"
        }
    ]
}
```

## ⚙ Setup

### 📝 Requisites

Antes de baixar o projeto você vai precisar ter instalado na sua máquina as seguintes ferramentas:

* [Git](https://git-scm.com)
* [NodeJS](https://nodejs.org/en/)
* [NPM](https://www.npmjs.com/), [PNPM](https://pnpm.io/pt/) ou [Yarn](https://yarnpkg.com/) 

Além disto é bom ter um editor para trabalhar com o código como [VSCode](https://code.visualstudio.com/)

Para testar as rotas da aplicação você pode usar o cliente HTTP [Postman](https://www.postman.com/)

### Cloning and Running

Passo a passo para clonar e executar a aplicação na sua máquina:

```bash
# Clone este repositório
$ git clone https://github.com/DanielEgiidio/planner_backend.git

# Instale as dependências
$ npm install

# Crie o arquivo '.env' e preencha as variáveis conforme o arquivo '.env.example' 

# Execute as migrations para criar as tabelas necessários no banco
$ npx prisma migrate-dev

# Execute a aplicação em modo de desenvolvimento
$ npm run dev

# A aplicação inciará na porta que você configurou no arquivo '.env' 
```


## 🛠 Technologies

As seguintes principais ferramentas foram usadas na construção do projeto:

- **[TypeScript](https://www.typescriptlang.org/)**
- **[Fastify](https://fastify.dev/)**
- **[Prisma](https://www.prisma.io/)**
- **[Zod](https://zod.dev/)**
- **[Nodemailer](https://nodemailer.com/)**
- **[DayJS](https://day.js.org/)**

> Para mais detalhes das dependências gerais da aplicação veja o arquivo [package.json](./package.json)


## 📝 License

Este projeto está sob a licença MIT. Consulte o arquivo [LICENSE](./LICENSE) para mais informações

