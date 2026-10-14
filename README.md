# NEXUS Network Monitor

Plataforma de monitoramento de redes, servidores e infraestrutura de TI (projeto de aprendizado e portfólio).

## Status atual: versão 0.1 (Fase 2: backend base)

| Item | Estado |
|---|---|
| API FastAPI: setup do admin, login/refresh/logout, RBAC | Escrito |
| CRUD de dispositivos, paginação, filtros, validação de IP (anti-SSRF) | Escrito |
| Modelos: usuários, dispositivos, verificações, eventos, auditoria | Escrito |
| Docker Compose (API + PostgreSQL + Redis) | Escrito |
| Testes automatizados (20) | Escritos, **ainda não executados pelo autor** |
| Worker de monitoramento (ICMP/SNMP), alertas | Pendente (Fase 3) |
| Frontend (dashboard), agente Windows/Linux | Pendente (Fases 4 e 5) |
| Migração Alembic inicial | Pendente (por ora `init_db` cria as tabelas) |

## Executar com Docker

PowerShell:
```powershell
Copy-Item .env.example .env   # edite e troque POSTGRES_PASSWORD
docker compose up -d --build
docker compose ps
docker compose logs -f api
```
Bash:
```bash
cp .env.example .env          # edite e troque POSTGRES_PASSWORD
docker compose up -d --build
```
API em http://127.0.0.1:8000 e Swagger em http://127.0.0.1:8000/docs (somente fora de produção).

## Primeiro administrador
```bash
curl -X POST http://127.0.0.1:8000/api/v1/setup -H "Content-Type: application/json" \
  -d '{"username":"admin","password":"UmaSenhaForte#2026"}'
```
Só funciona enquanto não existir nenhum usuário. Não há senha padrão.

## Testes (sem Docker)
```bash
cd backend
python -m venv .venv && source .venv/bin/activate   # Windows: .venv\Scripts\Activate.ps1
pip install -r requirements-dev.txt
pytest -q
```

## Limitações conhecidas
- Ainda não há coleta real de métricas: dispositivos cadastrados ficam com status `unknown` até a Fase 3.
- ICMP dentro de containers exige a capacidade `NET_RAW` e se comporta diferente no Docker Desktop/Windows.
- Limitador de login em memória (uma réplica da API).

Licença MIT. Veja `SECURITY.md`.
