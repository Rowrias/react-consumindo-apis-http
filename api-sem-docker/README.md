# 🚀 Code Connect Backend

Uma API REST para uma plataforma de compartilhamento de conteúdo sobre programação, construída com **NestJS**, **Prisma** e **SQLite**.

## 📋 Sobre o Projeto

O Code Connect é uma plataforma onde desenvolvedores podem compartilhar posts sobre programação, interagir através de comentários e curtidas. Esta é a API backend que fornece todos os endpoints necessários para:

- **Autenticação de usuários** (registro, login, JWT)
- **Gerenciamento de posts** (criar, listar, editar, excluir)
- **Sistema de comentários**
- **Sistema de curtidas**
- **Perfis de usuários**

## 🛠️ Tecnologias Utilizadas

- **[NestJS](https://nestjs.com/)** - Framework Node.js para APIs escaláveis
- **[Prisma](https://prisma.io/)** - ORM moderno para TypeScript/JavaScript
- **[SQLite](https://sqlite.org/)** - Banco de dados local (arquivo `dev.db`)
- **[JWT](https://jwt.io/)** - Autenticação via tokens
- **[bcrypt](https://www.npmjs.com/package/bcrypt)** - Hash de senhas
- **[TypeScript](https://www.typescriptlang.org/)** - Superset do JavaScript

## ⚡ Como Rodar o Projeto

### Pré-requisitos

- **Node.js** (versão 18 ou superior)
- **npm** ou **yarn**

### 🔧 Configuração

1. **Clone o repositório:**
```bash
git clone <url-do-repositorio>
cd code-connect-backend-node
```

2. **Instale as dependências:**
```bash
npm install
```

3. **Configure as variáveis de ambiente:**
O arquivo `.env` já está configurado com:
```
DATABASE_URL="file:./dev.db"
JWT_SECRET="your-secret-key-here"
```

4. **Execute as migrações e seeds:**
```bash
# Gera o banco de dados SQLite e aplica as migrações
npx prisma migrate dev

# Popula o banco com dados iniciais (usuários e posts de exemplo)
npx prisma db seed
```

### 🚀 Executando a Aplicação

```bash
# Modo desenvolvimento (com hot-reload)
npm run start:dev

# Modo produção
npm run build
npm run start:prod
```

A API estará disponível em: `http://localhost:3000`

## 📊 Banco de Dados

O projeto usa **SQLite** como banco de dados, o que significa:

- ✅ **Sem dependências externas** (não precisa instalar PostgreSQL, Docker, etc.)
- ✅ **Portabilidade total** - o banco é um arquivo (`prisma/dev.db`)
- ✅ **Fácil backup** - basta copiar o arquivo do banco
- ✅ **Perfeito para desenvolvimento** e pequenas aplicações

### Visualizando os dados

```bash
# Abrir interface gráfica do Prisma Studio
npx prisma studio
```

## 📁 Estrutura do Projeto

```
src/
├── auth/           # Módulo de autenticação
├── users/          # Módulo de usuários
├── posts/          # Módulo de posts
├── comments/       # Módulo de comentários  
├── prisma/         # Configurações do Prisma
└── main.ts         # Arquivo principal

prisma/
├── schema.prisma   # Schema do banco de dados
├── dev.db         # Banco SQLite (criado automaticamente)
├── migrations/    # Histórico de migrações
└── seed.ts        # Script de dados iniciais
```

## 🔐 Endpoints Principais

### Autenticação
- `POST /auth/register` - Cadastro de usuário
- `POST /auth/login` - Login e obtenção do JWT

### Posts
- `GET /posts` - Listar todos os posts
- `GET /posts/:id` - Obter post específico
- `POST /posts` - Criar novo post (autenticado)
- `PUT /posts/:id` - Editar post (autenticado)
- `DELETE /posts/:id` - Excluir post (autenticado)

### Comentários
- `GET /posts/:id/comments` - Listar comentários de um post
- `POST /posts/:id/comments` - Criar comentário (autenticado)
- `PUT /comments/:id` - Editar comentário (autenticado)
- `DELETE /comments/:id` - Excluir comentário (autenticado)

## 🧪 Dados de Exemplo

Após executar o seed, você terá:

- **4 usuários** de exemplo (senha: `123456`)
  - ana@codeconnect.com
  - bruno@codeconnect.com
  - carla@codeconnect.com
  - diego@codeconnect.com

- **12 posts** sobre diversos temas de programação
- **Comentários** aleatórios nos posts

## 🛠️ Comandos Úteis

```bash
# Instalar dependências
npm install

# Rodar em modo desenvolvimento
npm run start:dev

# Build para produção
npm run build

# Prisma - Gerar client
npx prisma generate

# Prisma - Aplicar migrações
npx prisma migrate dev

# Prisma - Resetar banco (cuidado!)
npx prisma migrate reset

# Prisma - Visualizar dados
npx prisma studio

# Rodar seeds novamente
npx prisma db seed

# Linting
npm run lint

# Testes
npm run test
```

## 🔄 Desenvolvimento

Para desenvolver novas funcionalidades:

1. **Modifique o schema** (`prisma/schema.prisma`)
2. **Crie uma migração:** `npx prisma migrate dev --name nome-da-migrao`
3. **Implemente os endpoints** nos controllers
4. **Teste** com Postman, Insomnia ou similar

## 💾 Backup e Migração

Para fazer backup dos dados:
```bash
# Copiar o banco
cp prisma/dev.db backup/dev-backup-$(date +%Y%m%d).db

# Ou exportar para SQL
sqlite3 prisma/dev.db .dump > backup/database-backup.sql
```

## 📝 Observações

- O banco SQLite é criado automaticamente na primeira execução
- Os dados persistem entre reinicializações da aplicação
- Para limpar todos os dados: `npx prisma migrate reset`
- Para ambiente de produção, considere PostgreSQL ou MySQL

---

✨ **Pronto para desenvolver!** A API está configurada e funcionando localmente sem nenhuma dependência externa.
