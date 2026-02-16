# 🚀 WORKFLOW DE SETUP DE PROJETO MONOREPO - ANTIGRAVITY

## 📋 VISÃO GERAL

Este documento define o **workflow padrão e reutilizável** para inicialização de projetos no Antigravity seguindo arquitetura monorepo com separação entre **Backend (NestJS + Railway + Supabase)** e **Mobile (React Native/Expo)**.

Use este guia como **checklist obrigatório** ao iniciar qualquer novo projeto.

---

## 🏗️ ESTRUTURA PADRÃO DO MONOREPO

```
[nome-do-projeto]/
├── backend/                    # API NestJS hospedada no Railway
│   ├── src/
│   │   ├── modules/           # Módulos de domínio (users, auth, etc.)
│   │   ├── shared/            # Código compartilhado (decorators, filters)
│   │   ├── config/            # Configurações (database, jwt, etc.)
│   │   ├── common/            # DTOs, interfaces, enums globais
│   │   └── main.ts            # Entry point da aplicação
│   ├── prisma/                # Schema Prisma + Migrations
│   │   ├── schema.prisma
│   │   └── migrations/
│   ├── test/                  # Testes E2E
│   ├── .env.example           # Template de variáveis de ambiente
│   ├── .env                   # Variáveis locais (gitignored)
│   ├── package.json
│   ├── tsconfig.json
│   ├── nest-cli.json
│   └── README.md
│
├── mobile/                     # App React Native com Expo
│   ├── app/                   # Expo Router (file-based routing)
│   │   ├── (tabs)/           # Rotas com bottom tabs
│   │   ├── (auth)/           # Rotas de autenticação
│   │   ├── _layout.tsx       # Root layout
│   │   └── +not-found.tsx    # 404 screen
│   ├── components/            # Componentes de UI
│   │   ├── ui/               # Componentes atômicos (Button, Input)
│   │   ├── forms/            # Formulários compostos
│   │   └── layout/           # Containers, Headers
│   ├── hooks/                 # Custom hooks
│   │   ├── useQuery/         # Queries com TanStack Query
│   │   └── useMutation/      # Mutations
│   ├── services/              # Clientes de API
│   │   ├── api/              # Axios/Fetch configurado
│   │   └── supabase.ts       # Cliente Supabase
│   ├── store/                 # Zustand stores
│   │   ├── authStore.ts
│   │   └── appStore.ts
│   ├── types/                 # TypeScript types compartilhados
│   │   ├── api/              # DTOs (sincronizados com backend)
│   │   ├── models/           # Domain models
│   │   └── navigation.ts     # Tipos de navegação
│   ├── utils/                 # Funções utilitárias
│   ├── assets/                # Imagens, fontes, ícones
│   ├── constants/             # Constantes da aplicação
│   ├── app.json               # Configuração do Expo
│   ├── package.json
│   ├── tsconfig.json
│   └── tailwind.config.js     # NativeWind config
│
├── .gitignore                 # Git ignore global do monorepo
├── docker-compose.yml         # (Opcional) Setup local com Docker
├── package.json               # (Opcional) Root package.json para scripts
├── RAILWAY_ENV.md             # Documentação de variáveis Railway
├── [projeto]_architecture.md  # Documentação da arquitetura
├── [projeto]_dev_planning.md  # Planejamento de desenvolvimento
├── [projeto]_prd_complete.md  # PRD (Product Requirements Document)
└── documento_nova_feature.md  # Template para novas features
```

---

## ✅ FASE 1: INICIALIZAÇÃO DO REPOSITÓRIO

### 1.1 Criar Estrutura Base

**Instruções para o Agente Antigravity:**

```plaintext
TAREFA: Inicializar monorepo com nome "[NOME_DO_PROJETO]"

1. Criar pasta raiz do projeto
2. Inicializar Git com branch main
3. Criar subpastas: backend/ e mobile/
4. Criar .gitignore global seguindo o template fornecido
5. Gerar documentos de projeto (ver seção 1.2)
```

**Template do .gitignore:**
```gitignore
# === DEPENDENCIES ===
node_modules/
.pnp
.pnp.js
.yarn/

# === ENVIRONMENT VARIABLES ===
.env
.env.local
.env.development.local
.env.test.local
.env.production.local

# === LOGS ===
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*

# === BUILD OUTPUTS ===
dist/
build/
.expo/
.expo-shared/
*.tsbuildinfo
.turbo/

# === TESTING ===
coverage/
*.lcov

# === OS SPECIFIC ===
.DS_Store
Thumbs.db
*.swp
*.swo
*~

# === IDE ===
.vscode/
.idea/
*.iml

# === MISC ===
.cache/
.parcel-cache/
```

### 1.2 Criar Documentos Essenciais

**Instruções para o Agente:**

```plaintext
TAREFA: Gerar 4 documentos de projeto na raiz

1. [PROJETO]_architecture.md - Descrever stack e arquitetura
2. [PROJETO]_dev_planning.md - Planejamento em sprints
3. [PROJETO]_prd_complete.md - Product Requirements Document
4. documento_nova_feature.md - Template reutilizável
5. RAILWAY_ENV.md - Variáveis de ambiente
```

**Template: [PROJETO]_architecture.md**
```markdown
# Arquitetura do [PROJETO]

## Stack Tecnológico

### Backend
- **Framework**: NestJS
- **Hospedagem**: Railway
- **Database**: Supabase (PostgreSQL)
- **ORM**: Prisma
- **Autenticação**: Supabase Auth + JWT

### Mobile
- **Framework**: React Native (Expo SDK 51+)
- **Roteamento**: Expo Router v3
- **State Management**: Zustand + TanStack Query
- **Styling**: NativeWind (Tailwind CSS)
- **Listas**: FlashList

## Fluxo de Dados
Mobile → API (Railway) → Database (Supabase)

## Módulos Principais
[Listar módulos do sistema]
```

**Template: [PROJETO]_dev_planning.md**
```markdown
# Planejamento de Desenvolvimento

## Sprint 1: Fundação (Semana 1-2)
- [ ] Setup do monorepo (backend + mobile)
- [ ] Configuração Railway + Supabase
- [ ] Sistema de autenticação
- [ ] Tela de login/registro

## Sprint 2: Features Core (Semana 3-4)
- [ ] [Feature 1]
- [ ] [Feature 2]

## Sprint 3: Refinamento (Semana 5-6)
- [ ] Melhorias de UX
- [ ] Testes
- [ ] Performance
```

**Template: documento_nova_feature.md**
```markdown
# Template: Nova Feature

## Nome da Feature
[Nome descritivo]

## Contexto
[Por que essa feature é necessária?]

## Especificação Técnica

### Backend (NestJS)
**Endpoints necessários**:
- `POST /api/[recurso]` - [Descrição]
- `GET /api/[recurso]` - [Descrição]

**DTOs**:
\```typescript
interface CreateXDto {
  campo: string;
}
\```

### Mobile (Expo)
**Telas**: `app/[nome-tela].tsx`
**Hooks**: `hooks/useQuery/useX.ts`

### Database
\```prisma
model X {
  id    String @id @default(uuid())
  campo String
}
\```

## Critérios de Aceite
- [ ] [Critério 1]
- [ ] [Critério 2]
```

**Template: RAILWAY_ENV.md**
```markdown
# Variáveis de Ambiente - Railway

## Backend
\```bash
DATABASE_URL=postgresql://...
SUPABASE_URL=https://[ID].supabase.co
SUPABASE_ANON_KEY=[KEY]
JWT_SECRET=[SECRET]
PORT=3000
\```

## Mobile (app.config.js)
\```javascript
extra: {
  apiUrl: "https://[app].railway.app",
  supabaseUrl: process.env.SUPABASE_URL,
}
\```
```

---

## 🔧 FASE 2: SETUP DO BACKEND (NestJS)

### 2.1 Inicializar Projeto NestJS

**Instruções para o Agente:**

```plaintext
TAREFA: Criar projeto NestJS na pasta backend/

1. Navegar para pasta backend/
2. Executar: npx @nestjs/cli new . --skip-git --package-manager npm
3. Instalar dependências essenciais (ver lista abaixo)
4. Criar estrutura de pastas (ver seção 2.2)
5. Configurar Prisma (ver seção 2.3)
6. Criar .env.example e .env
```

**Dependências Essenciais:**
```bash
# Core
npm install @nestjs/config @nestjs/swagger @nestjs/throttler

# Autenticação
npm install @nestjs/jwt @nestjs/passport passport passport-jwt
npm install -D @types/passport-jwt

# Validação
npm install class-validator class-transformer

# Database
npm install prisma @prisma/client

# Integração Supabase
npm install @supabase/supabase-js

# Segurança
npm install bcrypt
npm install -D @types/bcrypt
```

### 2.2 Estrutura de Pastas do Backend

**Instruções para o Agente:**

```plaintext
TAREFA: Criar estrutura de pastas em backend/src/

Executar comandos:
mkdir -p src/modules/{auth,users}
mkdir -p src/shared/{decorators,filters,guards,interceptors}
mkdir -p src/config
mkdir -p src/common/{dto,enums,interfaces}
```

**Estrutura resultante:**
```
backend/src/
├── modules/
│   ├── auth/
│   └── users/
├── shared/
│   ├── decorators/
│   ├── filters/
│   ├── guards/
│   └── interceptors/
├── config/
│   └── app.config.ts
├── common/
│   ├── dto/
│   ├── enums/
│   └── interfaces/
├── app.module.ts
└── main.ts
```

### 2.3 Configurar Prisma

**Instruções para o Agente:**

```plaintext
TAREFA: Setup Prisma ORM

1. Executar: npx prisma init
2. Substituir conteúdo de prisma/schema.prisma pelo template
3. Executar: npx prisma migrate dev --name init
4. Executar: npx prisma generate
```

**Template prisma/schema.prisma:**
```prisma
generator client {
  provider = "prisma-client-js"
}

datasource db {
  provider = "postgresql"
  url      = env("DATABASE_URL")
}

// Modelo base de exemplo
model User {
  id        String   @id @default(uuid())
  email     String   @unique
  password  String
  name      String?
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  @@map("users")
}
```

### 2.4 Configurar Arquivo de Configuração

**Arquivo: backend/src/config/app.config.ts**
```typescript
export default () => ({
  port: parseInt(process.env.PORT, 10) || 3000,
  nodeEnv: process.env.NODE_ENV || 'development',
  database: {
    url: process.env.DATABASE_URL,
  },
  supabase: {
    url: process.env.SUPABASE_URL,
    anonKey: process.env.SUPABASE_ANON_KEY,
    serviceKey: process.env.SUPABASE_SERVICE_KEY,
  },
  jwt: {
    secret: process.env.JWT_SECRET,
    expiresIn: process.env.JWT_EXPIRES_IN || '7d',
  },
});
```

### 2.5 Configurar main.ts para Produção

**Arquivo: backend/src/main.ts**
```typescript
import { NestFactory } from '@nestjs/core';
import { ValidationPipe } from '@nestjs/common';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';
import { AppModule } from './app.module';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  // CORS para mobile
  app.enableCors({
    origin: true,
    credentials: true,
  });

  // Global validation pipe
  app.useGlobalPipes(
    new ValidationPipe({
      whitelist: true,
      forbidNonWhitelisted: true,
      transform: true,
    }),
  );

  // Swagger (apenas em dev)
  if (process.env.NODE_ENV !== 'production') {
    const config = new DocumentBuilder()
      .setTitle('API Documentation')
      .setDescription('API endpoints description')
      .setVersion('1.0')
      .addBearerAuth()
      .build();
    const document = SwaggerModule.createDocument(app, config);
    SwaggerModule.setup('api/docs', app, document);
  }

  const port = process.env.PORT || 3000;
  await app.listen(port, '0.0.0.0');
  console.log(`🚀 Application running on: http://localhost:${port}`);
}
bootstrap();
```

### 2.6 Criar .env.example

**Arquivo: backend/.env.example**
```bash
# Database
DATABASE_URL="postgresql://user:password@localhost:5432/database"

# Supabase
SUPABASE_URL="https://[PROJECT_ID].supabase.co"
SUPABASE_ANON_KEY="your_anon_key"
SUPABASE_SERVICE_KEY="your_service_key"

# JWT
JWT_SECRET="your_jwt_secret_key_min_256_bits"
JWT_EXPIRES_IN="7d"

# App
NODE_ENV="development"
PORT=3000
```

**Instruções para o Agente:**
```plaintext
Após criar .env.example:
1. Copiar para .env: cp .env.example .env
2. Informar ao desenvolvedor para preencher as credenciais reais
```

---

## 📱 FASE 3: SETUP DO MOBILE (EXPO)

### 3.1 Criar Projeto Expo

**Instruções para o Agente:**

```plaintext
TAREFA: Criar projeto Expo na pasta mobile/

1. Navegar para pasta mobile/
2. Executar: npx create-expo-app@latest . --template blank-typescript
3. Instalar todas as dependências essenciais (ver lista abaixo)
4. Configurar NativeWind (ver seção 3.2)
5. Configurar Expo Router (ver seção 3.3)
```

**Dependências Essenciais:**
```bash
# Expo Router
npx expo install expo-router react-native-safe-area-context react-native-screens expo-linking expo-constants expo-status-bar

# Storage e Imagem
npx expo install expo-secure-store expo-image

# State Management
npm install zustand @tanstack/react-query

# HTTP Client
npm install axios

# Supabase
npm install @supabase/supabase-js

# Styling (NativeWind)
npm install nativewind
npm install --save-dev tailwindcss@3.3.2

# Performance (Listas)
npm install @shopify/flash-list

# Forms
npm install react-hook-form @hookform/resolvers zod

# Ícones
npx expo install @expo/vector-icons
```

### 3.2 Configurar NativeWind (Tailwind CSS)

**Instruções para o Agente:**

```plaintext
TAREFA: Setup NativeWind

1. Criar arquivo tailwind.config.js na raiz de mobile/
2. Criar arquivo nativewind-env.d.ts
3. Atualizar babel.config.js
```

**Arquivo: mobile/tailwind.config.js**
```javascript
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./App.{js,jsx,ts,tsx}",
    "./app/**/*.{js,jsx,ts,tsx}",
    "./components/**/*.{js,jsx,ts,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

**Arquivo: mobile/nativewind-env.d.ts**
```typescript
/// <reference types="nativewind/types" />
```

**Atualizar: mobile/babel.config.js**
```javascript
module.exports = function(api) {
  api.cache(true);
  return {
    presets: ['babel-preset-expo'],
    plugins: ['nativewind/babel'],
  };
};
```

### 3.3 Configurar Expo Router

**Instruções para o Agente:**

```plaintext
TAREFA: Setup Expo Router com estrutura de pastas

1. Criar estrutura de rotas (ver abaixo)
2. Criar _layout.tsx raiz com QueryClientProvider
3. Criar index.tsx inicial
4. Atualizar package.json main entry
```

**Comandos para estrutura:**
```bash
mkdir -p app/{,\(tabs\),\(auth\)}
mkdir -p components/{ui,forms,layout}
mkdir -p hooks/{useQuery,useMutation}
mkdir -p services/api
mkdir -p store
mkdir -p types/{api,models}
mkdir -p utils
mkdir -p constants
```

**Arquivo: mobile/app/_layout.tsx**
```typescript
import { Slot } from 'expo-router';
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import { StatusBar } from 'expo-status-bar';

const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      retry: 2,
      staleTime: 5 * 60 * 1000, // 5 minutos
    },
  },
});

export default function RootLayout() {
  return (
    <QueryClientProvider client={queryClient}>
      <StatusBar style="auto" />
      <Slot />
    </QueryClientProvider>
  );
}
```

**Arquivo: mobile/app/index.tsx**
```typescript
import { View, Text } from 'react-native';

export default function HomeScreen() {
  return (
    <View className="flex-1 justify-center items-center bg-white">
      <Text className="text-2xl font-bold">Welcome! 🚀</Text>
    </View>
  );
}
```

**Atualizar package.json:**
```json
{
  "main": "expo-router/entry"
}
```

### 3.4 Configurar API Client

**Arquivo: mobile/services/api/client.ts**
```typescript
import axios from 'axios';
import Constants from 'expo-constants';
import * as SecureStore from 'expo-secure-store';

const apiUrl = Constants.expoConfig?.extra?.apiUrl || 'http://localhost:3000';

export const apiClient = axios.create({
  baseURL: apiUrl,
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json',
  },
});

// Request interceptor - adiciona token
apiClient.interceptors.request.use(
  async (config) => {
    const token = await SecureStore.getItemAsync('auth_token');
    if (token) {
      config.headers.Authorization = `Bearer ${token}`;
    }
    return config;
  },
  (error) => Promise.reject(error)
);

// Response interceptor - trata 401
apiClient.interceptors.response.use(
  (response) => response,
  async (error) => {
    if (error.response?.status === 401) {
      await SecureStore.deleteItemAsync('auth_token');
      // TODO: Redirecionar para login
    }
    return Promise.reject(error);
  }
);
```

### 3.5 Configurar app.json

**Arquivo: mobile/app.json**
```json
{
  "expo": {
    "name": "[Nome do App]",
    "slug": "[slug-do-app]",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "userInterfaceStyle": "automatic",
    "splash": {
      "image": "./assets/splash.png",
      "resizeMode": "contain",
      "backgroundColor": "#ffffff"
    },
    "assetBundlePatterns": ["**/*"],
    "ios": {
      "supportsTablet": true,
      "bundleIdentifier": "com.empresa.app"
    },
    "android": {
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#ffffff"
      },
      "package": "com.empresa.app"
    },
    "scheme": "myapp",
    "plugins": [
      "expo-router",
      "expo-secure-store"
    ],
    "experiments": {
      "typedRoutes": true
    },
    "extra": {
      "router": {
        "origin": false
      },
      "apiUrl": "http://localhost:3000",
      "supabaseUrl": "",
      "supabaseAnonKey": "",
      "eas": {
        "projectId": ""
      }
    }
  }
}
```

**Instruções para o Agente:**
```plaintext
Após criar app.json:
- Preencher nome, slug e bundleIdentifier com valores do projeto
- Informar desenvolvedor para configurar extra.apiUrl com URL do Railway
```

---

## 🔗 FASE 4: INTEGRAÇÃO BACKEND ↔ MOBILE

### 4.1 Sincronizar DTOs (TypeScript Types)

**Princípio Fundamental:**
> Os DTOs do backend devem ser **espelhados** no mobile para garantir type safety completo.

**Instruções para o Agente:**

```plaintext
TAREFA: Para cada DTO criado no backend, criar versão correspondente no mobile

Exemplo:
Backend: backend/src/common/dto/user.dto.ts
Mobile:  mobile/types/api/user.dto.ts

⚠️ REGRA: Manter sincronização rigorosa entre os dois
```

**Exemplo de DTO no Backend:**
```typescript
// backend/src/common/dto/user.dto.ts
import { ApiProperty } from '@nestjs/swagger';
import { IsEmail, IsString } from 'class-validator';

export class UserDto {
  @ApiProperty()
  id: string;

  @ApiProperty()
  email: string;

  @ApiProperty()
  name: string | null;

  @ApiProperty()
  createdAt: Date;
}

export class CreateUserDto {
  @ApiProperty()
  @IsEmail()
  email: string;

  @ApiProperty()
  @IsString()
  password: string;
}
```

**Mesmo DTO no Mobile:**
```typescript
// mobile/types/api/user.dto.ts
// ⚠️ SINCRONIZADO COM backend/src/common/dto/user.dto.ts

export interface UserDto {
  id: string;
  email: string;
  name: string | null;
  createdAt: string; // Date vira string após serialização JSON
}

export interface CreateUserDto {
  email: string;
  password: string;
}
```

### 4.2 Padrão de Comunicação Mobile → Backend

**Instruções para o Agente:**

```plaintext
FLUXO PADRÃO:

1. Backend expõe endpoint: POST /api/users
2. Backend define CreateUserDto e UserDto
3. Mobile cria hooks correspondentes:
   - hooks/useMutation/useCreateUser.ts
   - hooks/useQuery/useUsers.ts
4. Mobile consome endpoint usando tipos sincronizados
```

**Exemplo Completo:**

**Backend: Endpoint**
```typescript
// backend/src/modules/users/users.controller.ts
@Post()
async create(@Body() dto: CreateUserDto): Promise<UserDto> {
  return this.usersService.create(dto);
}
```

**Mobile: Hook**
```typescript
// mobile/hooks/useMutation/useCreateUser.ts
import { useMutation } from '@tanstack/react-query';
import { apiClient } from '@/services/api/client';
import type { CreateUserDto, UserDto } from '@/types/api/user.dto';

export function useCreateUser() {
  return useMutation({
    mutationFn: async (dto: CreateUserDto) => {
      const { data } = await apiClient.post<UserDto>('/users', dto);
      return data;
    },
  });
}
```

### 4.3 Criar Package.json Raiz (Opcional)

**Instruções para o Agente:**

```plaintext
TAREFA: Criar package.json na raiz para scripts unificados

Permite executar comandos do monorepo de forma centralizada
```

**Arquivo: package.json (raiz)**
```json
{
  "name": "monorepo-root",
  "private": true,
  "scripts": {
    "backend:dev": "cd backend && npm run start:dev",
    "mobile:dev": "cd mobile && npm start",
    "backend:build": "cd backend && npm run build",
    "typecheck": "npm run typecheck:backend && npm run typecheck:mobile",
    "typecheck:backend": "cd backend && npx tsc --noEmit",
    "typecheck:mobile": "cd mobile && npx tsc --noEmit",
    "install:all": "cd backend && npm install && cd ../mobile && npm install"
  }
}
```

---

## 🚀 FASE 5: CONFIGURAÇÃO PARA DEPLOY

### 5.1 Preparar Backend para Railway

**Instruções para o Agente:**

```plaintext
TAREFA: Otimizar backend para Railway

1. Adicionar script start:prod ao package.json
2. Criar Procfile (opcional, Railway detecta automaticamente)
3. Verificar que main.ts escuta em 0.0.0.0
```

**Adicionar ao backend/package.json:**
```json
{
  "scripts": {
    "start:prod": "node dist/main"
  }
}
```

**Arquivo: backend/Procfile (opcional)**
```
web: npm run start:prod
```

### 5.2 Checklist de Deploy Railway

**Instruções para o Desenvolvedor:**

```plaintext
RAILWAY DEPLOY CHECKLIST:

1. Criar conta no Railway (railway.app)
2. Conectar repositório GitHub
3. Selecionar pasta /backend como root directory
4. Configurar variáveis de ambiente:
   - DATABASE_URL (do Supabase)
   - SUPABASE_URL
   - SUPABASE_ANON_KEY
   - JWT_SECRET
5. Railway faz deploy automático
6. Copiar URL gerada: https://[app].railway.app
```

### 5.3 Configurar EAS Build (Mobile)

**Instruções para o Agente:**

```plaintext
TAREFA: Setup EAS (Expo Application Services)

1. Instalar EAS CLI globalmente: npm install -g eas-cli
2. Fazer login: eas login
3. Configurar projeto: eas build:configure
4. Criar eas.json com perfis de build
```

**Arquivo: mobile/eas.json**
```json
{
  "cli": {
    "version": ">= 5.0.0"
  },
  "build": {
    "development": {
      "developmentClient": true,
      "distribution": "internal"
    },
    "preview": {
      "distribution": "internal",
      "env": {
        "API_URL": "https://[sua-app].railway.app"
      }
    },
    "production": {
      "env": {
        "API_URL": "https://[sua-app].railway.app"
      }
    }
  }
}
```

---

## ✅ CHECKLIST COMPLETO DE SETUP

### Backend ✓
- [ ] Projeto NestJS inicializado
- [ ] Dependências instaladas (@nestjs/config, prisma, etc.)
- [ ] Estrutura de pastas criada (modules, shared, config)
- [ ] Prisma configurado e primeira migration executada
- [ ] .env.example e .env criados
- [ ] main.ts configurado com CORS e Swagger
- [ ] app.config.ts com variáveis de ambiente
- [ ] README.md do backend criado

### Mobile ✓
- [ ] Projeto Expo TypeScript criado
- [ ] Dependências instaladas (expo-router, zustand, etc.)
- [ ] NativeWind configurado (tailwind.config.js, babel.config.js)
- [ ] Expo Router configurado (_layout.tsx, estrutura de pastas)
- [ ] TanStack Query configurado no root layout
- [ ] API client com interceptors (services/api/client.ts)
- [ ] app.json configurado com scheme e plugins
- [ ] package.json com main: "expo-router/entry"

### Integração ✓
- [ ] DTOs criados no backend
- [ ] DTOs espelhados no mobile (types/api/)
- [ ] API URL configurada no mobile (app.json extra.apiUrl)
- [ ] Teste de conectividade backend ↔ mobile realizado

### Documentação ✓
- [ ] .gitignore global criado
- [ ] [projeto]_architecture.md criado
- [ ] [projeto]_dev_planning.md criado
- [ ] [projeto]_prd_complete.md criado
- [ ] documento_nova_feature.md criado
- [ ] RAILWAY_ENV.md criado

### Git ✓
- [ ] Repositório inicializado
- [ ] Primeiro commit realizado
- [ ] Repositório GitHub criado e conectado
- [ ] README.md principal criado

---

## 🎯 COMANDOS RÁPIDOS DE REFERÊNCIA

### Backend
```bash
# Desenvolvimento
cd backend
npm run start:dev        # Modo watch
npm run build            # Build produção
npm run start:prod       # Rodar build

# Prisma
npx prisma studio        # UI do database
npx prisma migrate dev   # Nova migration
npx prisma generate      # Regenerar client
```

### Mobile
```bash
# Desenvolvimento
cd mobile
npm start                # Abrir menu Expo
npm run android          # Android emulator
npm run ios              # iOS simulator

# Build
eas build --platform android
eas build --platform ios
```

### Monorepo (na raiz)
```bash
npm run backend:dev      # Iniciar backend
npm run mobile:dev       # Iniciar mobile
npm run typecheck        # Verificar tipos
npm run install:all      # Instalar tudo
```

---

## 🆘 TROUBLESHOOTING COMUM

### Erro: "Cannot find module"
```bash
# Backend
cd backend && rm -rf node_modules dist && npm install

# Mobile
cd mobile && rm -rf node_modules .expo && npm install
npx expo start -c
```

### Erro: "Prisma Client did not initialize"
```bash
cd backend
npx prisma generate
npm run start:dev
```

### Erro: "Metro bundler failed to start"
```bash
cd mobile
npx expo start -c  # Limpar cache
```

### Erro: "Network request failed" no mobile
```plaintext
1. Verificar se backend está rodando (http://localhost:3000)
2. No Android Emulator, usar 10.0.2.2 ao invés de localhost
3. Verificar app.json extra.apiUrl
```

---

## 📚 REFERÊNCIAS E DOCUMENTAÇÃO

- **NestJS**: https://docs.nestjs.com/
- **Expo**: https://docs.expo.dev/
- **Expo Router**: https://docs.expo.dev/router/introduction/
- **Prisma**: https://www.prisma.io/docs
- **Railway**: https://docs.railway.app/
- **TanStack Query**: https://tanstack.com/query/latest
- **NativeWind**: https://www.nativewind.dev/
- **Zustand**: https://zustand-demo.pmnd.rs/

---

## 🎉 PRÓXIMOS PASSOS APÓS SETUP

Com o monorepo configurado, você está pronto para:

1. **Implementar Autenticação**
   - Backend: Módulo auth com JWT
   - Mobile: Telas de login/registro + authStore

2. **Criar Primeiros CRUDs**
   - Backend: Controllers + Services + DTOs
   - Mobile: Hooks + Telas + Componentes

3. **Deploy em Produção**
   - Backend: Railway deploy
   - Mobile: EAS Build

4. **Adicionar Novas Features**
   - Usar template documento_nova_feature.md

---

**✨ Workflow criado para Antigravity**  
**Versão**: 1.0  
**Tipo**: Template Reutilizável  
**Última atualização**: Fevereiro 2025

---

## 💡 DICAS PARA USO NO ANTIGRAVITY

### Para o Agente de Setup:
```plaintext
Ao receber comando "Inicializar projeto [NOME]":

1. Ler este workflow completo
2. Executar FASE 1 (Repo setup)
3. Executar FASE 2 (Backend setup)
4. Executar FASE 3 (Mobile setup)
5. Executar FASE 4 (Integração)
6. Gerar relatório final com checklist
7. Informar próximos passos ao desenvolvedor
```

### Para o Desenvolvedor:
```plaintext
Este workflow é um CHECKLIST VIVO:

- Use-o como guia ao iniciar projetos
- Customize conforme necessidade do projeto específico
- Mantenha sincronizado com atualizações de stack
- Compartilhe com time para padronização
```
