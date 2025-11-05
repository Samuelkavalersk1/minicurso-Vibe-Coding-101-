# ADR 001: Implementação de Autenticação Google-only

## Status
Aceito

## Contexto
O sistema necessita de um mecanismo de autenticação seguro e de fácil manutenção. Precisamos considerar a experiência do usuário, segurança e custos de implementação/manutenção.

## Decisão
Implementaremos autenticação exclusivamente através do Google OAuth2 usando FastAPI, eliminando a necessidade de autenticação própria.

### Detalhes Técnicos
- Uso do FastAPI com python-jose para JWT
- Google OAuth2 como único provedor de identidade
- Armazenamento mínimo de dados do usuário (apenas email e ID do Google)
- Sessions baseadas em JWT

## Consequências

### Positivas
- Eliminação da necessidade de gerenciar senhas
- Redução de riscos de segurança
- Processo de login familiar aos usuários
- Implementação e manutenção simplificadas
- Two-factor authentication automaticamente disponível via Google

### Negativas
- Dependência total do Google como provedor
- Usuários precisam ter conta Google
- Possível resistência de usuários preocupados com privacidade

## Alternativas Consideradas
1. Auth0 - Descartado por custos
2. Autenticação própria - Descartado por complexidade
3. Múltiplos provedores OAuth - Descartado por complexidade inicial

## Implementação

### Dependências Necessárias
```python
fastapi
python-jose[cryptography]
httpx
python-multipart
```

### Configuração Necessária
- Registro do aplicativo no Google Cloud Console
- Configuração de credenciais OAuth2
- Definição de URLs de callback
- Configuração de variáveis de ambiente para credenciais

## Métricas de Sucesso
- Taxa de sucesso em logins > 99%
- Tempo médio de login < 3 segundos
- Zero incidentes de segurança relacionados à autenticação
