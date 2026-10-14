# Política de segurança

- Use o NEXUS apenas em redes e equipamentos que você está autorizado a monitorar.
- Nunca suba o arquivo `.env` ou segredos para o repositório.
- Em produção: defina `NEXUS_JWT_SECRET` (mínimo 32 caracteres), use HTTPS (proxy reverso) e não exponha PostgreSQL nem Redis.
- Para reportar uma vulnerabilidade, abra uma *security advisory* privada no GitHub do projeto.
