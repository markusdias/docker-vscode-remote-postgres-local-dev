# Ambiente de Desenvolvimento com VSCode Server e PostgreSQL

Este projeto fornece um ambiente de desenvolvimento completo com:
- **VSCode Server**: IDE acessível via navegador
- **PostgreSQL**: Banco de dados relacional
- **pgAdmin**: Interface gráfica para gerenciamento do PostgreSQL

## Requisitos

- Docker e Docker Compose instalados
- Git (para versionamento do código)

## Configuração Inicial

1. Clone o repositório:
```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
```

2. Crie o arquivo `.env` com as credenciais:
```bash
cp .env.example .env
```

3. Edite o arquivo `.env` com suas credenciais desejadas

## Uso Básico

Iniciar o ambiente:
```bash
docker-compose up -d
```

Parar o ambiente:
```bash
docker-compose down
```

Ver logs:
```bash
docker-compose logs -f
```

## Acessos

- **VSCode Server**: http://localhost:8080
  - Senha: Definida no arquivo `.env` (VSCODE_PASSWORD)
  
- **PostgreSQL**: localhost:5432
  - Credenciais no arquivo `.env` (POSTGRES_*)

- **pgAdmin**: http://localhost:5050
  - Credenciais no arquivo `.env` (PGADMIN_*)

## Estrutura do Projeto

```
.
├── .env               # Variáveis de ambiente
├── docker-compose.yml # Configuração dos containers
└── README.md          # Este arquivo
```

## Persistência de Dados

Todos os dados importantes são armazenados em volumes Docker:
- `code-server-data`: Workspace do VSCode
- `postgres-data`: Dados do PostgreSQL
- `pgadmin-data`: Configurações do pgAdmin

Para backup:
```bash
# PostgreSQL
docker exec -t postgres pg_dumpall -c -U ${POSTGRES_USER} > dump_$(date +%Y-%m-%d).sql

# code-server (se necessário)
docker run --rm -v code-server-data:/volume -v $(pwd):/backup alpine tar cvf /backup/code-server-backup.tar /volume
```

## Considerações Finais

- O código fonte deve ser versionado no GitHub/GitLab
- Nunca versionar o arquivo `.env`
- Adicionar `.env` ao `.gitignore`
- Fazer backups periódicos dos volumes
