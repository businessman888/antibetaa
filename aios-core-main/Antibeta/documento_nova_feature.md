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
```typescript
interface CreateXDto {
  campo: string;
}
```

### Mobile (Expo)
**Telas**: `app/[nome-tela].tsx`
**Hooks**: `hooks/useQuery/useX.ts`

### Database
```prisma
model X {
  id    String @id @default(uuid())
  campo String
}
```

## Critérios de Aceite
- [ ] [Critério 1]
- [ ] [Critério 2]
