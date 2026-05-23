# Contexto do Projeto — DespachaTudo APP

## Identificação

- **Natureza**: Startup / produto digital em co-construção (não cliente convencional)
- **Papel de Heverton**: Designer e PM (gerenciamento de produto e design)
- **Status atual**: MVP em produção, bloqueio crítico no WhatsApp API (mai/2026)
- **Site**: https://www.despachatudo.com.br
- **Figma**: https://www.figma.com/design/PwyylsADkSRTK1kT26hxfz/DespachaTudo
- **Data de entrada**: fev/2026 (primeiras conversas registradas 06/02/2026)

## Proposta de Valor

Aplicativo para despachantes (agentes de habilitação e licenciamento veicular). Automatiza atendimento via WhatsApp Business API com chatbot GPT, reduzindo tempo de resposta e aumentando conversão de clientes.

## Time do Projeto

| Pessoa | Papel | Contato |
|---|---|---|
| Maurício Primo | Fundador / financiador | WhatsApp (número que detém o WABA) |
| Heverton | Designer / PM | hevertonmac@gmail.com |
| Rafael Macedo | Desenvolvedor full-stack | Desenvolveu site + chatbot |
| Lúcio Vieira | Marketing / Meta setup | Configurou Business Manager Meta |
| Marcela Santana | Jurídico / legal | Emitiu NF para Backup Design (R$2.000 abr/2026) |

## Stack Tecnológica

- **Chatbot**: GPT integrado via Typebot
- **WhatsApp**: Meta WhatsApp Business API (WABA)
- **Site**: despachatudo.com.br (servidor gratuito — tier free, sujeito a limitações)
- **Design**: Figma (protótipo completo disponível)
- **Hospedagem atual**: servidor gratuito (ponto de atenção para escalabilidade)

## Histórico de Marcos (fev–mai/2026)

- **Fev/2026**: Início do projeto, primeiros alinhamentos de produto e design
- **Mar/2026**: Prototipação no Figma, definição do fluxo do chatbot
- **Abr/2026**: Marcela Santana emite NF — Backup Design recebe R$2.000 pelo trabalho
- **Mai/2026**: Site no ar (despachatudo.com.br). Rafael finaliza integração do chatbot. Lúcio configura o Business Manager da Meta.

## Bloqueio Crítico (status em 22/05/2026)

**Problema**: O token de acesso do WhatsApp Business API ainda não foi gerado/verificado.

**Causa raiz**:
1. Lúcio criou um novo Business Manager (BM) na Meta
2. O número de WhatsApp que será vinculado ao WABA pertence a Maurício Primo
3. A verificação do número exige ação direta de Maurício (receber código no celular)
4. Rafael aguarda o token/secret para conectar o chatbot — sem isso o sistema não funciona de ponta a ponta

**Próximos passos para desbloquear**:
- Maurício deve acessar o Meta BM criado por Lúcio
- Verificar o número no fluxo oficial do WhatsApp Business API
- Lúcio gerar o token permanente e repassar para Rafael
- Rafael finalizar a conexão Typebot ↔ WABA

## Modelo Comercial / Remuneração

- Heverton não tem participação societária documentada nesta fase
- Recebimento via NF emitida pela Backup Design LTDA (Marcela Santana pagou R$2.000 em abr/2026)
- Modelo de continuidade não definido explicitamente nas conversas analisadas

## Observações Estratégicas

- Servidor gratuito é um risco para o MVP — ao crescer, haverá necessidade de upgrade de infraestrutura
- O produto tem potencial real: despachantes são um nicho com volume e recorrência
- Heverton acumula design + PM, o que aumenta seu valor e sua carga
- A dependência de Maurício para o número WABA é o único bloqueio técnico restante
