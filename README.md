# Agents Project - Backend

Uma API REST inteligente para criação e gerenciamento de agentes educacionais baseados em IA. O sistema permite upload de conteúdo em áudio, transcrição automática, busca semântica e geração de respostas contextualizadas utilizando o Google Gemini AI.

## 🎯 Sobre o Projeto

O Agents Backend é uma solução completa para criar assistentes educacionais inteligentes que podem:

- **Processar Áudio**: Upload e transcrição automática de arquivos de áudio
- **Busca Semântica**: Utiliza embeddings para encontrar conteúdo relevante
- **Respostas Contextualizadas**: Gera respostas baseadas no conteúdo fornecido
- **Organização por Salas**: Gerencia diferentes contextos educacionais
- **Histórico de Perguntas**: Mantém registro das interações

### Funcionalidades Principais

- 📁 **Gerenciamento de Salas**: Crie ambientes isolados para diferentes conteúdos
- 🎙️ **Transcrição de Áudio**: Converte automaticamente áudio em texto (PT-BR)
- 🔍 **Busca Vetorial**: Encontra conteúdo relevante usando similaridade semântica
- 🤖 **IA Conversacional**: Responde perguntas baseadas no conteúdo transcrito
- 📊 **Histórico**: Mantém registro de todas as perguntas e respostas

## 🛠️ Tecnologias Utilizadas

- **Node.js** v20+ (com TypeScript nativo)
- **Fastify** - Framework web rápido e eficiente
- **TypeScript** - Linguagem com tipagem estática
- **PostgreSQL** - Banco de dados relacional
- **pgvector** - Extensão para busca vetorial
- **Drizzle ORM** - ORM moderno para TypeScript
- **Google Gemini AI** - IA para transcrição e geração de respostas
- **Zod** - Validação de esquemas
- **Docker** - Containerização

## 📁 Estrutura do Projeto

```
src/
├── db/
│   ├── connection.ts      # Conexão com banco
│   ├── schema/           # Esquemas do banco
│   │   ├── rooms.ts      # Schema de salas
│   │   ├── questions.ts  # Schema de perguntas
│   │   └── audio-chunks.ts # Schema de chunks de áudio
│   └── migrations/       # Migrações do banco
├── http/
│   └── routes/          # Rotas da API
│       ├── get-rooms.ts
│       ├── create-room.ts
│       ├── get-room-questions.ts
│       ├── create-question.ts
│       └── upload-audio.ts
├── services/
│   └── gemini.ts        # Integração com Google Gemini
├── env.ts               # Configuração de ambiente
└── server.ts           # Servidor principal
```

## 🚀 Setup e Configuração

### 1. Pré-requisitos

- **Node.js** v20 ou superior
- **Docker** e **Docker Compose**
- **Conta Google Cloud** com API Gemini habilitada

### 2. Clonar o Repositório

```bash
git clone <repository-url>
cd agents-backend
```

### 3. Instalar Dependências

```bash
npm install
```

### 4. Configurar Variáveis de Ambiente

Crie um arquivo `.env` na raiz do projeto:

```env
# Configuração do servidor HTTP
PORT=3333

# Configuração do banco de dados
DATABASE_URL="postgresql://docker:docker@localhost:5432/agents_project"

# Chave da API do Google Gemini
GOOGLE_GENAI_API_KEY=sua_chave_aqui
```

**⚠️ Importante**: Obtenha sua chave da API do Google Gemini em [Google AI Studio](https://aistudio.google.com/app/apikey)

### 5. Configurar e Iniciar o Banco de Dados

```bash
# Inicie o PostgreSQL com pgvector usando Docker
docker-compose up -d

# Aguarde alguns segundos para o banco inicializar completamente
```

### 6. Executar Migrações

```bash
# Execute as migrações do banco de dados
npx drizzle-kit migrate
```

### 7. Popular o Banco (Opcional)

```bash
# Execute o seed para criar dados de exemplo
npm run db:seed
```

### 8. Executar a Aplicação

```bash
# Desenvolvimento (com watch mode e reload automático)
npm run dev

# Produção
npm start
```

A API estará disponível em `http://localhost:3333`

## 📋 Endpoints Disponíveis

### Saúde da Aplicação
- `GET /health` - Health check da aplicação

### Salas (Rooms)
- `GET /rooms` - Lista todas as salas com contagem de perguntas
- `POST /room` - Cria uma nova sala

### Perguntas
- `GET /room/:roomId/questions` - Lista perguntas de uma sala
- `POST /room/:roomId/questions` - Cria nova pergunta e gera resposta

### Áudio
- `POST /room/:roomId/audio` - Upload de áudio para transcrição

## 🧪 Testando a API

Utilize o arquivo [`client.http`](client.http) para testar os endpoints:

```bash
# Instale a extensão REST Client no VS Code
# Ou use curl/Postman com os exemplos do arquivo
```

## 🏗️ Fluxo de Funcionamento

1. **Criação de Sala**: Crie uma sala para organizar o conteúdo
2. **Upload de Áudio**: Envie arquivos de áudio para transcrição
3. **Processamento**: O sistema transcreve e gera embeddings
4. **Pergunta**: Faça perguntas sobre o conteúdo
5. **Resposta**: Receba respostas contextualizadas baseadas no áudio

## 🗄️ Banco de Dados

O projeto utiliza PostgreSQL com a extensão **pgvector** para busca vetorial. O esquema inclui:

- **rooms** - Salas para organizar conteúdo
- **questions** - Perguntas e respostas dos usuários
- **audio_chunks** - Chunks de áudio transcritos com embeddings

## 📝 Scripts Disponíveis

- `npm run dev` - Executa em modo desenvolvimento com reload automático
- `npm start` - Executa em modo produção
- `npm run db:seed` - Popula o banco com dados iniciais
- `npx drizzle-kit migrate` - Executa migrações do banco
- `npx drizzle-kit studio` - Abre interface visual do banco

## 🔧 Configuração Adicional

### Docker Compose

O projeto inclui configuração Docker para PostgreSQL com pgvector:

```yaml
# docker-compose.yml
services:
  postgres:
    image: pgvector/pgvector:pg16
    # ... outras configurações
```

### Migrações

As migrações são gerenciadas automaticamente pelo Drizzle Kit:

```bash
# Gerar nova migração
npx drizzle-kit generate

# Aplicar migrações
npx drizzle-kit migrate
```

## 🤝 Contribuindo

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -am 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request
