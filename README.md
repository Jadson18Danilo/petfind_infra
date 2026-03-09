# Petfind Infra (Docker Compose)

Este diretório centraliza a orquestração Docker do monorepo (`frontend` + `backend` + `postgres` + `adminer`).

## Pré-requisitos

- Docker Desktop instalado e em execução
- Docker Compose v2 (`docker compose`)

## Estrutura conectada

- `frontend`: build de `../petfind_frontend/Dockerfile`
- `backend`: build de `../petfind_backend/Dockerfile`
- `postgres`: imagem oficial `postgres:15`
- `adminer`: imagem oficial `adminer`

## Comandos principais

> Execute todos os comandos abaixo dentro de `petfind_infra`.

### Porta do backend (evita conflito)

Por padrão, o backend Docker publica em `4001` (não `4000`) para não conflitar com um backend local em desenvolvimento.

Se quiser trocar, crie um arquivo `.env` em `petfind_infra` com:

```powershell
BACKEND_HOST_PORT=4010
```

### Subir tudo

```powershell
docker compose up -d
```

### Ver status dos serviços

```powershell
docker compose ps
```

### Ver logs (todos)

```powershell
docker compose logs -f
```

### Ver logs por serviço

```powershell
docker compose logs -f backend
docker compose logs -f frontend
docker compose logs -f postgres
docker compose logs -f adminer
```

### Rebuild das imagens

```powershell
docker compose build --no-cache
docker compose up -d
```

### Parar mantendo volumes

```powershell
docker compose down
```

### Parar e remover volumes (reset de banco)

```powershell
docker compose down -v
```

## Portas padrão

- Frontend (Docker): `http://localhost:5424`
- Backend (Docker): `http://localhost:4001`
- Adminer: `http://localhost:8080`
- Postgres (host): `localhost:5433`

## Observações

- O backend roda migrações automaticamente no startup (`npm run db:migrate && npm start`).
- Uploads do backend persistem no volume `backend_uploads`.
- Dados do Postgres persistem no volume `postgres_data`.
- O frontend local com `npm run dev` segue em `http://localhost:5423`.
