# Pedidos Veloz 🚀

Sistema de microsserviços para gerenciamento de pedidos.

## Arquitetura

Cliente → Gateway → Pedidos
├── Pagamentos
├── Estoque
└── PostgreSQL

## Serviços

| Serviço    | Porta | Descrição                        |
|------------|-------|----------------------------------|
| Gateway    | 3000  | Roteamento de requisições        |
| Pedidos    | 3001  | Criação e gestão de pedidos      |
| Pagamentos | 3002  | Processamento de pagamentos      |
| Estoque    | 3003  | Controle de estoque              |
| PostgreSQL | 5432  | Banco de dados                   |
| RabbitMQ   | 5672  | Mensageria                       |

## Tecnologias

- Node.js + TypeScript
- Express
- Prisma + PostgreSQL
- RabbitMQ
- Docker + Docker Compose
- Kubernetes
- GitHub Actions

## Como rodar

### Pré-requisitos

- Docker
- Docker Compose

### Subir o projeto

```bash
git clone https://github.com/arthurreleven/pedidos_veloz
cd pedidos_veloz
docker compose up --build
```

### Testar

```bash
# Criar pedido
curl -X POST http://localhost:3001/pedido \
  -H "Content-Type: application/json" \
  -d '{"produto":"Teclado","quantidade":2,"valor":500}'

# Listar pedidos
curl http://localhost:3001/pedido
```

## Variáveis de ambiente

Crie um arquivo `.env` na raiz com:

```env
POSTGRES_USER=admin
POSTGRES_PASSWORD=suasenha
POSTGRES_DB=pedidos_db
```

## Kubernetes

```bash
kubectl apply -f k8s/secret.yaml
kubectl apply -f k8s/configmap.yaml
kubectl apply -f k8s/postgres/
kubectl apply -f k8s/pedidos/
kubectl apply -f k8s/pagamentos/
kubectl apply -f k8s/estoque/
kubectl apply -f k8s/gateway/
```

## CI/CD

Pipeline automático via GitHub Actions a cada push na branch `main`:

- Instala dependências
- Build das imagens Docker

## Segurança

- Containers rodando com usuário não-root (`USER node`)
- Credenciais via variáveis de ambiente
- Secrets do Kubernetes para dados sensíveis