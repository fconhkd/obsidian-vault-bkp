---
title: 03 - Fundamentos de Perícia Forense Digital
date: 2025-11-08 20:02
url: https://www.youtube.com/watch?v=K5_-jovtGKI&list=PLIfZMtpPYFP5Y_xDxvK1yO9aDxZvM8fB3
tags:
  - CYBERSECURITY
  - DEFENSIVE
  - DFIR
aliases:
  - Foco no processo de pericia e construção do relatório de incidente e sua apresentação
---
## Introdução

A aula apresenta os **fundamentos da perícia forense digital,** abordando desde conceitos básicos até procedimentos práticos aplicados em resposta a incidentes de segurança. O conteúdo cobre princípios como o de Locard, legislações brasileiras relevantes, histórico da perícia digital e as seis fases do processo forense, com foco na coleta e preservação de evidências digitais.

## Aula 03 - DFIR

![DFIR - Aula 3](https://www.youtube.com/watch?v=K5_-jovtGKI&list=PLIfZMtpPYFP5Y_xDxvK1yO9aDxZvM8fB3)

### 🎯 Destaques do vídeo

[00:00:03](https://copilot.microsoft.com/chats/xcfofV6nh3W8dcM8dzLLy#timestamp-00:00:03) **Introdução e objetivos da aula**

- Aula 3 do curso DFIR, voltada à perícia digital
- Apresentação dos fundamentos da ciência forense
- Aplicações em resposta a incidentes de segurança

[00:01:08](https://copilot.microsoft.com/chats/xcfofV6nh3W8dcM8dzLLy#timestamp-00:01:08) **Conceito de ciência forense**

- Aplicação da ciência em contextos legais
- Coleta e análise de evidências físicas e digitais
- Produção de laudos e relatórios periciais

[00:03:30](https://copilot.microsoft.com/chats/xcfofV6nh3W8dcM8dzLLy#timestamp-00:03:30) **Princípio de Locard**

- Todo contato deixa um rastro (exemplos de digitais em copos)
- Aplicação tanto no mundo físico quanto digital
- Logs, IPs e credenciais como vestígios digitais

[00:05:17](https://copilot.microsoft.com/chats/xcfofV6nh3W8dcM8dzLLy#timestamp-00:05:17) **Legislação brasileira aplicável**

- Código de Processo Penal do Exame de Corpo de Delito e Pericias em Geral
- ECA - Lei 8069 de 13 de julho de 19990 (Pedofilia)
- Marco Civil da Internet - Lei 12.965 de 23 de abril de 2014
- Lei Carolina Dieckmann - Lei 12.737 de 30 de novembro de 2012
- LGPD - Lei 13.709 de 14 de agosto de 2018
- ISO 27037 - Diretrizes de atuação forense
- Cadeia de custódia (Portaria 82/2014 SENASP)
- Procedimentos operacionais padrão (POP-SENASP/MJ)

[00:08:36](https://copilot.microsoft.com/chats/xcfofV6nh3W8dcM8dzLLy#timestamp-00:08:36) **Histórico da perícia digital**

- Início nos anos 1980 com crimes cibernéticos
- Casos marcantes como o hacker do Macros e o worm Morris
- Evolução da atuação de órgãos como FBI e Polícia Federal

[00:10:45](https://copilot.microsoft.com/chats/xcfofV6nh3W8dcM8dzLLy#timestamp-00:10:45) **As 6 fases da perícia digital**

- Identificação, preservação, coleta, exame, análise e apresentação
- Importância da documentação e da cadeia de custódia
- Ferramentas e técnicas específicas para cada fase

## Processo de Forense em Resposta a Incidentes

Parecido com o processo de RI, o processo define o fluxo de evidencias digitais relacionadas a um incidente que é identificado pela primeira vez até a apresentação a um tribunal, utiliza-se a estrutura da investigação digital (DFRWS) que incorpora as 6 fases

- Identificação -  é aqui que o principio de Locard entra em jogo
- Preservação - Identificar as evidencias e protege-las
- Coleta - Aquisição de evidencias (RFC 3227) considerando a sua volatidade (cadeia de custodia)
- Exame - Detalha as ferramentas as técnicas forenses utilizadas para coletar por parte o incidente
- Analise - Realizar a coleta dos dados de informações e cruzar com fontes adicionais para determinar maiores informações (exemplo coletar o IP e cruzar com bases de fora para detalhar a reputação)
- Apresentação - Relatório da pericia deve ser clara, concisa e imparcial, abordando todas as ações de capturas dos dados críticos abordando todas as ações (testemunho em tribunal caso judicial) 

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
