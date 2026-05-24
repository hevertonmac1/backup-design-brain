# Skill 07 — Acesso ao Second Brain em Nova Sessão

**Objetivo:** Protocolo para qualquer sessão de IA acessar o Second Brain automaticamente.

---

## Onde ficam as coisas

| Item | Caminho no Mac |
|------|---------------|
| PAT (token GitHub) | `~/Documents/Claude/Projects/Second Brain/.pat` |
| Memória permanente | `~/Documents/Claude/Projects/Second Brain/MEMORY.md` |
| Clone de trabalho | `/tmp/brain/` |
| Repositório GitHub | `https://github.com/hevertonmac1/backup-design-brain` |

> **Atenção:** O filesystem montado NAO suporta git clone (erro .git/config.lock). O clone SEMPRE vai para /tmp/brain.

---

## Protocolo de Inicio de Sessao

```bash
# Passo 1 — Ler o PAT salvo localmente
PAT=$(cat "$HOME/Documents/Claude/Projects/Second Brain/.pat" | tr -d '\n')

# Passo 2 — Clonar ou atualizar
if [ -d "/tmp/brain/.git" ]; then
  git -C /tmp/brain pull
else
  git clone "https://${PAT}@github.com/hevertonmac1/backup-design-brain.git" /tmp/brain
fi

# Passo 3 — Verificar
ls /tmp/brain/ && cat /tmp/brain/mapa_geral.md
```

---

## Leitura Obrigatoria Apos Clone

1. mapa_geral.md — visao geral completa
2. 01_Contexto_Geral/ — contexto pessoal e empresarial
3. 04_Clientes_Ativos/mapa.md — estado atual dos clientes
4. 00_Inbox/contexto_gemini_mai2026.md — briefing completo para IA

---

## Como Commitar e Fazer Push

```bash
cd /tmp/brain
git add .
git commit -m "descricao das mudancas"

PAT=$(cat "$HOME/Documents/Claude/Projects/Second Brain/.pat" | tr -d '\n')
git remote set-url origin "https://${PAT}@github.com/hevertonmac1/backup-design-brain.git"
git push origin main
```

> NUNCA colocar o PAT real dentro de nenhum arquivo do repositorio.
> Usar sempre o placeholder SEU_PAT_AQUI em documentacao.

---

## Erros Comuns

| Erro | Causa | Solucao |
|------|-------|---------|
| .git/config.lock: Operation not permitted | Clone no filesystem montado | Clonar sempre em /tmp/brain |
| Authentication failed | PAT expirado | Heverton gera novo PAT e atualiza .pat |
| remote: Push cannot contain secrets | PAT real no commit | Substituir por SEU_PAT_AQUI |
| /tmp/brain vazio | Diretorio temporario limpo | Normal — re-clonar no inicio |

---

## Seguranca — Regras Permanentes

- SEU_PAT_AQUI — placeholder para docs dentro do repo
- .pat — unico lugar com token real, local, nunca commitado
- CNPJ 15.760.736/0001-35 — MANTER (necessario para contexto de IA)
- WhatsApp pessoal — omitido por seguranca
- Emails pessoais de terceiros — email omitido
