---
title: 01-Introdução
date: 2026-01-17 18:29
url-code:
tags:
  - PROJECT
aliases:
---
## 🎯Objetivo

Este projeto tem como objetivo desenvolver uma plataforma web voltada para auditorias de conformidade em diferentes frameworks de segurança e privacidade. A proposta central é permitir que um cliente receba um link único, realize seu cadastro e responda a um conjunto de perguntas específicas. A partir dessas respostas, o sistema calcula automaticamente o nível de conformidade (score) do cliente, oferecendo uma visão clara sobre sua maturidade em relação ao framework selecionado.

A solução é pensada para ser **genérica, modular e expansível**, permitindo que novos frameworks sejam adicionados com facilidade. Inicialmente, o foco está em três referências amplamente utilizadas no mercado:

- **CIS Controls v8**    
- **LGPD**    
- **PCI-DSS**    

A plataforma busca simplificar o processo de auditoria, padronizar avaliações e fornecer relatórios consistentes e automatizados.

## 📅 Status

Criado apenas para testar, crie aqui o seu conteúdo e descreva par ajudar a pensar no futuro.

```dataview
table 
    round((completed / total) * 100) as "Progresso (%)"
from "Projetos/Auditoria"
where file.name = this.file.name
flatten length(filter(file.tasks, (t) => t.completed)) as completed
flatten length(file.tasks) as total
```

## 🗂️ Próximas ações

- [ ] Primeira ação clara e executável
- [ ] Outra ação importante
- [ ] Algo que dependa de outra pessoa

## 📚 Referências

- [Manual de Controles CIS v8 (CIS Controls)](https://www.gov.br/sudeco/pt-br/acesso-a-informacao/comite-de-governanca-riscos-controle-e-integridade-da-sudeco/copy_of_ManualdeControlesCISverso8_SEI0328545.pdf)
- [Site oficial do PCI Security Standards Council (PCI-DSS)](https://www.pcisecuritystandards.org/lang/pt-pt/)
- [Lei de Portabilidade e Responsabilidade de Seguros de Saúde dos EUA (HIPAA)](https://www.congress.gov/crs_external_products/IF/PDF/IF12759/IF12759.1.pdf)
- 

## Histórico

- 2026-01-16 — Reunião no discord para falar da ferramenta
- 2026-01-17 — Inicio das pesquisas
- 2026-01-17 — Registro rápido do que foi feito ou decidido

## Timeline do projeto

```chronos
@ [2026-01-01~2026-02-15] {Inicio} 01
- [2026-01-16] {Inicio} "Ideia inicial (CIS v8)"
- [2026-01-17~2026-01-31] {Inicio} Pesquisas
- [2026-02-01~2026-02-15] {Inicio} Documentar
  
@ [2026-02-16~2026-03-18] {Desenvolvimento} 02
- [2026-02-16~2026-03-01] {Desenvolvimento} Backend
- [2026-03-02~2026-03-18] {Desenvolvimento} Front
  
@ [2026-03-19~2026-06-19] {Testes} 03
- [2026-03-19~2026-04-15] {Testes} CIS v8
- [2026-04-16~2026-05-15] {Testes} PCI-DSS v4.0
- [2026-05-16~2026-05-30] {Testes} Corrigir
- [2026-06-01~2026-06-19] {Testes} PCI-DSS v4.1
  
@ [2026-06-20~2026-06-30] {Lançamento} 04
- [2026-06-30] {Lançamento} Produção
```

## 🧠 Notas

-

---
## Referencias
### Internas
```dataview
list
from [[]]
```

### Links
```dataview
table
title as Titulo, length(file.inlinks) as Referencias, tags as Tags
from [[]]
```
