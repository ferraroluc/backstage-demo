# Demo for Backstage

Base code for Backstage, both as a mono and multi repo.

## Database for Docker

For using with Docker, is necessary to run a PostgreSQL database.

```bash
docker network create backstage
docker run -d --name backstage-postgres --network backstage --restart=always -p 5432:5432 -e POSTGRES_PASSWORD=postgres postgres:17.0-bookworm
```

## Monorepo

Use one repo for Backend and Frontend.

### Local

```bash
cd monorepo
yarn install
yarn dev
```

### Docker

```bash
cd monorepo
yarn install --immutable
yarn tsc
yarn build:backend
yarn build-image
docker run -it -p 7007:7007 --network backstage backstage-monorepo
```

## Multirepo

Split project between Backend and Frontend.

### Backend

#### Local

```bash
cd only-backend
yarn install
yarn dev
```

#### Docker

```bash
cd only-backend
yarn install --immutable
yarn tsc
yarn build:backend
yarn build-image
docker run -it -p 7007:7007 --network backstage backstage-backend
```

### Frontend

#### Local

```bash
cd only-frontend
yarn install
yarn dev
```

#### Docker

```bash
cd only-frontend
yarn install --immutable
yarn tsc
yarn build
yarn build-image
docker run -it -p 3000:80 --network backstage backstage-frontend
```
