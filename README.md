
# Métricas Coolify (Prometheus + Grafana + Loki + Promtail)

Stack de observabilidade para monitorar containers do Coolify e o host Ubuntu.

## O que está incluso
- **Prometheus** (coleta de métricas) — **não exposto externamente**
- **Grafana** (dashboards) — **porta 3000 exposta**
- **Loki** (logs) — **não exposto externamente**
- **Promtail** (agente de logs)
- **Node Exporter** (métricas do host)
- **cAdvisor** (métricas de containers)
- **Dashboards JSON** pré-carregados (Host, Containers, Logs)

## Subindo a stack
1. Opcional: crie um `.env` a partir do exemplo
   ```bash
   cp .env.example .env
   ```
2. Suba os serviços
   ```bash
   docker compose up -d
   ```
3. Acesse o Grafana em `http://SEU_IP:3000` (admin / senha do `.env` ou `admin`).

## Criar o repositório no GitHub (via GitHub CLI)
> Recomendado usar um nome sem espaços/acentos, ex.: `metricas-coolify`.

```bash
# dentro da pasta do projeto
gh repo create metricas-coolify --private --source=. --remote=origin --push
```

Se preferir criar primeiro e depois enviar:
```bash
gh repo create metricas-coolify --private -y
git init && git add . && git commit -m "Monitoring: Prometheus, Grafana, Loki, Promtail"
git branch -M main
git remote add origin git@github.com:SEU_USUARIO/metricas-coolify.git
git push -u origin main
```

## Dashboards incluídos
- `Host Overview (Node Exporter)` — CPU, memória, disco, rede
- `Containers Overview (cAdvisor)` — CPU, memória e IO por container
- `Logs Explorer (Loki)` — filtro por container

## Segurança
- Exposto apenas o **Grafana (3000)**; mantenha firewall ativo.
- Altere a senha padrão do Grafana.

## Uso com Coolify
- Importe este repositório como **Application → Docker Compose**.
- Variáveis de ambiente podem ser configuradas pelo Coolify (ex.: `GF_SECURITY_ADMIN_PASSWORD`).

Licença: MIT
