# Skill 06 — Operação do Second Brain por IA

Documento de aprendizado técnico e operacional para uso por qualquer instância de IA
que seja acionada para trabalhar neste repositório.
Criado em mai/2026 com base em sessões extensas de construção e manutenção do brain.

---

## 1. ACESSO AO REPOSITÓRIO

**Repositório GitHub**: https://github.com/hevertonmac1/backup-design-brain
**PAT (Personal Access Token)**: SEU_PAT_AQUI
**Branch principal**: main

### Como clonar corretamente

```bash
git clone https://SEU_PAT_AQUI@github.com/hevertonmac1/backup-design-brain.git /tmp/brain
```

**CRITICO**: Sempre clonar em `/tmp/brain`. NUNCA clonar em `/sessions/.../outputs`.
O diretório outputs causa erros de permissão com `.git/config.lock` que impedem commits.

### Configurar identidade Git antes do primeiro commit

```bash
git -C /tmp/brain config user.email "hevertonmac@gmail.com"
git -C /tmp/brain config user.name "Heverton Andrade"
```

### Ciclo de trabalho padrão

```bash
# 1. Verificar estado atual
git -C /tmp/brain status --short

# 2. Adicionar tudo
git -C /tmp/brain add -A

# 3. Commitar
git -C /tmp/brain commit -m "Brain: [descricao objetiva do que foi feito]"

# 4. Enviar
git -C /tmp/brain push origin main
```

**Padrão de mensagem de commit**: sempre iniciar com `Brain:` seguido de descrição clara do conteúdo adicionado ou modificado.

---

## 2. ESTRUTURA DO REPOSITÓRIO

```
backup-design-brain/
├── mapa_geral.md              ← leitura obrigatória antes de qualquer operação
├── 00_Inbox/                  ← entradas brutas, rascunhos, inteligência temporária
├── 01_Contexto_Geral/         ← identidade da empresa, contexto pessoal, time, fiscal
├── 02_Skills/                 ← playbooks operacionais (este arquivo está aqui)
├── 03_Arquivos_Cold_Storage/  ← clientes encerrados, histórico inativo
├── 04_Clientes_Ativos/        ← clientes com contrato, prospecção ativa ou sociedade
└── 05_Projetos/               ← projetos de equity/parceria estratégica
```

### Regra estrutural invariável

Toda pasta tem um `mapa.md`. Nunca criar pasta sem criar o `mapa.md` correspondente.
O `mapa.md` lista o propósito da pasta e todos os arquivos/subpastas com uma linha de descrição.

### Hierarquia de leitura antes de qualquer operação

1. `mapa_geral.md`
2. `mapa.md` da pasta onde vai trabalhar
3. Arquivo específico relevante

---

## 3. REGRAS DE ESCRITA E ESTILO

- **Sem emojis** em nenhum arquivo do repositório — regra absoluta
- **Sem acentos obrigatórios** — os arquivos usam texto sem acentuação para evitar problemas de encoding no Git. Usar "sócio" → "socio", "ação" → "acao", etc.
- **Tom**: executivo, direto, minimalista. Sem linguagem informal.
- **Cabeçalho padrão de arquivo**:
  ```
  # Titulo do Arquivo — Contexto
  **Status**: STATUS ATUAL
  **[campo relevante]**: valor
  ---
  ```
- **Tabelas Markdown** para dados estruturados (cronologias, pessoas, financeiro)
- **Seções com ##** para hierarquia clara

---

## 4. CLASSIFICAÇÃO DE CLIENTES

### Onde cada cliente vai

| Situação | Pasta |
|---|---|
| Contrato ativo, cobrança recorrente | `04_Clientes_Ativos/` |
| Prospecção em andamento | `04_Clientes_Ativos/` (status = PROSPECCAO) |
| Sociedade com equity | `04_Clientes_Ativos/` ou `05_Projetos/` |
| Projeto encerrado, entregue ou contrato finalizado | `03_Arquivos_Cold_Storage/` |
| Histórico sem atividade relevante | `03_Arquivos_Cold_Storage/` |

### Estrutura padrão de pasta de cliente

```
04_Clientes_Ativos/NomeCliente/
├── contexto_cliente.md    ← histórico, contatos, projeto, financeiro, papel de Heverton
└── mapa.md                ← status resumido e lista de arquivos
```

### Campos obrigatórios em contexto_cliente.md

1. Status atual (ATIVO / PROSPECCAO / ENCERRADO)
2. Identificação (empresa, contatos, setor)
3. Papel de Heverton no projeto
4. Serviços/entregas
5. Cronologia (tabela de datas/marcos)
6. Financeiro (modelo, valores, pagamentos)
7. Notas estratégicas

---

## 5. LEITURA DE GMAIL

O Gmail de Heverton está disponível via MCP connector:
`mcp__26d1a164-50d9-4284-a414-5ed9c832f76f__search_threads`

**Parâmetro correto**: `pageSize` (máximo 50). NÃO usar `maxResults`.

### Estratégia de varredura completa (quando necessário)

Para cobrir um período extenso (ex: 18 meses), fazer buscas por faixas de tempo e filtros:

```
# Por período + remetente/domínio
after:2025/01/01 before:2025/04/01

# Emails enviados (mais confiáveis para rastrear clientes ativos)
in:sent after:2025/01/01 before:2025/07/01

# Por cliente específico
from:cliente@dominio.com OR to:cliente@dominio.com
```

- Resultados grandes (>20KB) são salvos em arquivos persistidos — usar `Read` tool no caminho retornado
- Sempre buscar também `in:sent` — os emails enviados revelam quem Heverton estava atendendo ativamente
- Cruzar dados de múltiplas buscas antes de concluir que um cliente não existe

### O que procurar em cada email

- Nome do cliente / empresa
- Tipo de serviço prestado
- Datas de início e fim
- Pagamentos mencionados
- Pessoas envolvidas (nome + email)
- Status do projeto

---

## 6. PADRÕES APRENDIDOS NESTE REPOSITÓRIO

### Sobre a operação geral

- Heverton opera em múltiplas frentes simultâneas — sempre registrar todas no contexto pessoal
- Clientes internacionais chegam principalmente via Gerard Rogan (99designs) e via indicações
- O modelo mais lucrativo atual: retainer em dólar (Wicks + Stimpson = $1.790/mês)
- Smartleader é emprego principal mas gera conflito de agenda — documentar sempre como "gargalo ativo"
- DespachaTudo é sociedade (50%) — nunca tratar como cliente convencional

### Sobre movimentação de clientes entre pastas

Quando um cliente muda de status:
1. Mover a pasta inteira com `cp -r` + `rm -rf` (não renomear — git detecta como delete+create, mas está correto)
2. Atualizar o `contexto_cliente.md` com novo status e informações adicionais
3. Atualizar o `mapa.md` da pasta de origem (remover entrada)
4. Atualizar o `mapa.md` da pasta de destino (adicionar entrada)
5. Commitar tudo junto em um único commit

### Sobre o arquivo de contexto para IAs externas

Manter atualizado: `00_Inbox/contexto_gemini_mai2026.md`
Este arquivo é o briefing completo usado para onboarding de sessões em outros modelos (Gemini, ChatGPT, etc.).
Deve ser regenerado sempre que houver mudanças estruturais significativas no brain.

---

## 7. ERROS COMUNS E COMO EVITAR

| Erro | Causa | Solução |
|---|---|---|
| `git: cannot lock ref` ou erros de permissão no .git | Clone feito em `/sessions/.../outputs` | Sempre clonar em `/tmp/brain` |
| Arquivo com acentos causando problemas | Encoding inconsistente | Escrever sem acentos em todos os arquivos .md do repo |
| Commit sem arquivos no stage | `git add` não foi executado | Sempre verificar `git status --short` antes de commitar |
| Pasta criada sem mapa.md | Esqueceu a regra estrutural | Após `mkdir`, imediatamente criar o `mapa.md` |
| Cliente classificado errado | Não verificou status real antes de mover | Perguntar ao Heverton se o status não estiver claro |
| Contexto incompleto do cliente | Só leu emails recentes | Sempre buscar `in:sent` + período completo + nome do cliente |
| Clone perdido entre sessões | `/tmp/` é limpo entre sessões | Sempre verificar se `/tmp/brain` existe no início de cada sessão; se não, clonar novamente |

---

## 8. CHECKLIST DE INÍCIO DE SESSÃO

Executar no início de qualquer sessão de trabalho no brain:

```bash
# 1. Verificar se o clone existe
ls /tmp/brain/ 2>/dev/null && echo "EXISTS" || echo "MISSING"

# 2. Se missing, clonar
git clone https://SEU_PAT_AQUI@github.com/hevertonmac1/backup-design-brain.git /tmp/brain

# 3. Verificar estado (arquivos uncommitted de sessão anterior?)
git -C /tmp/brain status --short

# 4. Ler mapa_geral.md
cat /tmp/brain/mapa_geral.md
```

---

## 9. CHECKLIST DE ENCERRAMENTO DE SESSÃO

Antes de terminar qualquer sessão:

```bash
# Garantir que tudo está commitado e enviado
git -C /tmp/brain status --short
git -C /tmp/brain add -A
git -C /tmp/brain commit -m "Brain: [resumo do que foi feito na sessão]"
git -C /tmp/brain push origin main
```

Nunca encerrar sessão com arquivos não commitados.

---

## 10. HIERARQUIA DE PRIORIDADE AO RECEBER INSTRUCAO

Quando Heverton der uma instrução, seguir esta ordem:

1. Verificar se o repositório está atualizado (`git pull` se necessário)
2. Ler o `mapa.md` da área afetada antes de escrever qualquer arquivo
3. Perguntar sobre status real do cliente SE não estiver claro (nunca classificar por suposição)
4. Criar/editar arquivos
5. Atualizar todos os `mapa.md` afetados
6. Commitar e fazer push
7. Confirmar com número do commit

