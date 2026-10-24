# InfoÁgua

Monitoramento colaborativo do abastecimento e da qualidade da água, com previsão do tempo local.

<!-- ![InfoÁgua](docs/screenshot.png) -->

Os moradores relatam no mapa quando falta água, quando o abastecimento volta, vazamentos e problemas de qualidade. Os outros usuários acompanham, curtem e comentam as ocorrências.

Projeto da disciplina de **Desenvolvimento de Dispositivos Móveis** (DDM) — IFRN.

## Funcionalidades

- **Relatar ocorrência** com tipo, descrição, foto e localização: falta d'água, retorno do abastecimento, vazamento ou problema de qualidade
- **Mapa** com as ocorrências e filtro por tipo
- **Histórico** com as ocorrências que você relatou
- **Curtidas e comentários** em cada ocorrência
- **Clima** da localização atual via OpenWeather
- **Conta de usuário** com cadastro, login (JWT) e perfil público
- **API documentada** com Swagger

## Stack

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript&logoColor=white&style=for-the-badge) ![NestJS](https://img.shields.io/badge/NestJS-E0234E?logo=nestjs&logoColor=white&style=for-the-badge) ![Prisma](https://img.shields.io/badge/Prisma-2D3748?logo=prisma&logoColor=white&style=for-the-badge) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?logo=postgresql&logoColor=white&style=for-the-badge) ![MinIO](https://img.shields.io/badge/MinIO-C72E49?logo=minio&logoColor=white&style=for-the-badge) ![React Native](https://img.shields.io/badge/React_Native-20232A?logo=react&logoColor=61DAFB&style=for-the-badge) ![Expo](https://img.shields.io/badge/Expo-000020?logo=expo&logoColor=white&style=for-the-badge) ![Swagger](https://img.shields.io/badge/Swagger-85EA2D?logo=swagger&logoColor=black&style=for-the-badge) ![Jest](https://img.shields.io/badge/Jest-C21325?logo=jest&logoColor=white&style=for-the-badge) ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white&style=for-the-badge) ![OpenWeather](https://img.shields.io/badge/OpenWeather-EB6E4B?style=for-the-badge) ![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?logo=githubactions&logoColor=white&style=for-the-badge)

## Como rodar

Você precisa de [Node.js](https://nodejs.org/) (LTS), [Docker](https://www.docker.com/) e do app [Expo Go](https://expo.dev/go) no celular, ou de um emulador Android/iOS.

### 1. Infraestrutura (PostgreSQL e MinIO)

```bash
cd infra
cp .env.example .env   # senhas e chave da API do OpenWeather
docker compose up -d db minio
```

### 2. Backend

```bash
cd backend
cp .env.example .env   # use os mesmos valores do .env da infra
npm install
npx prisma migrate dev
npm run start:dev
```

A API sobe em `http://localhost:3000/v1`, e a documentação fica em `http://localhost:3000/api/docs`.

### 3. App mobile

```bash
cd mobile
npm install
npm run start
```

Depois, aperte `a` para abrir no emulador Android, `i` para o simulador iOS, ou escaneie o QR Code com o Expo Go.

No emulador Android o app já aponta para `10.0.2.2:3000`. Num celular físico, crie um `mobile/.env` com o IP da sua máquina:

```bash
EXPO_PUBLIC_API_URL=http://192.168.0.10:3000/v1
```

### Testes

```bash
cd backend
npm test           # unitários
npm run test:e2e   # ponta a ponta
```

## Estrutura

```
infra/     Docker Compose com PostgreSQL e MinIO
backend/   API REST em NestJS: auth, ocorrências, comentários, curtidas, upload e clima
mobile/    app em React Native com Expo Router
```

O GitHub Actions roda lint, build e testes a cada push e pull request.
