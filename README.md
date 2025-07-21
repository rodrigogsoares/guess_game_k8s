<<<<<<< HEAD
# Projeto Guess Game - Ambiente em Docker
Este projeto contém a infraestrutura completa para subir uma aplicação web com frontend em React, backend em Flask e banco de dados PostgreSQL, com balanceamento de carga e proxy reverso via NGINX.

## Visão Geral

Esta aplicação implementa um jogo de adivinhação utilizando:
- **Backend:** Python + Flask
- **Frontend:** React
- **Banco de Dados:** PostgreSQL para persistência de dados
- **Proxy Reverso:** NGINX com balanceamento de carga

## Arquitetura da Solução

### Serviços

| Serviço              | Função                                                                 |
|----------------------|------------------------------------------------------------------------|
| `db`                 | Banco de dados PostgreSQL para persistência de dados                   |
| `backend1`, `backend2` | Aplicações Flask que processam a lógica da API                        |
| `frontend`           | Container NGINX que serve a aplicação React **e** faz proxy para o backend |

**Obs.: Todos os serviços têm `restart: always` para ter resiliência.

---

### Volumes Persistentes

- O banco de dados usa volume `postgres_data`, garantindo persistência entre reinicializações.

---

### Network

- Todos os serviços estão na **mesma rede Docker interna** permitindo que se comuniquem por nomes de serviço (ex: `postgres`, `backend1`, `backend2`).

---

### Balanceamento de Carga

O serviço `frontend` usa o NGINX como **Proxy reverso** para rotear chamadas `/api/` para o backend e **Balanceador de carga** entre dois containers do backend (`backend1` e `backend2`).

---

## Como Executar

### 1. Requisitos
- Docker
- Docker Compose v2+

### 2. Faça o Git Clone do repositório e execute:
```bash
git clone https://github.com/rodrigogsoares/guess_game
cd guess_game
docker compose up --build -d
```

Acesse o jogo em: [http://localhost:3000](http://localhost:3000)

## Atualização de Componentes

**Backend**:
- Edite `Dockerfile.backend` ou `requirements.txt`
- Rebuild apenas os containers do backend:

```bash
docker-compose build backend1 backend2
docker-compose up -d
```

**Frontend**:
- Edite `Dockerfile.frontend` ou código React
- Rebuild o frontend:

```bash
docker-compose build frontend
docker-compose up -d
```

**DB (PostgreSQL)**:
- Mude a versão da imagem Postgres no `docker-compose.yml`

```bash
db:
  image: postgres:17-alpine  # nova versão desejada
```

- Baixe a nova imagem e reinicie:

```bash
docker-compose pull db
docker-compose up -d
```

- **NGINX**: edite `frontend/nginx.conf`


## Derrubar os serviços

```bash
docker-compose down
```

## Observações Finais

Para alterar o IP de API do Backend que o Frontend utiliza, ajuste no arquivo Dockerfile.frontend, conforme exemplo abaixo

```bash
ARG REACT_APP_BACKEND_URL=http://localhost:5000
```
=======
# guess_game_k8s
Guess Game K8S
>>>>>>> b46867b0eee3230508d8ee8053a7bb8f7dfcd757
