---
title: Por onde começar no obsidian
date: 2026-01-17 17:53
url:
tags:
  - OBSIDIAN
  - NOTES
  - REMEMBER
aliases:
  - Obsisian o inicio
---
## Introdução

Criei essa nota para me lembrar de como usar o Obsidian no dia-a-dia para criar minhas anotações, vou tentar ir colocando aqui o que vou me lembrando e o que não posso esquecer.

# 🧭 Guia Pessoal do Meu Obsidian

Este arquivo reúne tudo que preciso lembrar sobre como uso o Obsidian: meus padrões, atalhos, templates, convenções e boas práticas. É meu manual de referência rápida.

## 📂 Estrutura das Minhas Notas

- **Áreas** → temas contínuos (saúde, finanças, trabalho, estudos)
- **Inbox** → onde coloco tudo que ainda não processei    
- **Query** → notas diárias, reflexões, logs
	- **Referência** → conhecimento permanente
- **Projetos** → cada projeto com sua própria pasta    

## 🔗 Como Uso Links Internos

- `[[Nome da Nota]]` para conectar ideias    
- `[[2026-01-17]]` para navegar entre dias    
- `![[arquivo.png]]` para embedar imagens    
- Links bidirecionais para criar contexto automático

## ⚡ Atalhos Importantes

- **Ctrl + O** → abrir nota rapidamente    
- **Ctrl + N** → nova nota    
- **Ctrl + Shift + F** → busca global    
- **Ctrl + P** → comandos    
- **Ctrl + E** → alternar entre edição e visualização   

## 🧠 Meu Fluxo de Trabalho

1. **Capturar** tudo na Inbox    
2. **Processar** no fim do dia    
3. **Organizar** em Projetos / Áreas / Referências    
4. **Revisar** semanalmente    
5. **Arquivar** o que não é mais útil

## 📊 Exemplos de Consultas Dataview

### Tarefas Pendentes

dataview

```
task
where !completed
sort file.ctime desc
```

### Projetos Ativos

dataview

```
list from "Projetos"
where contains(Status, "Em andamento")
```

## Criar um Template

Criei uma pasta Template e adicionei o meu modelo lá dentro, toda ves que for criar um novo documento tenho que me lembrar de aplicar o meu template nesse arquivo e adicionar as Tags e comentários para ir gerando o histórico do que fui estudando e apredendo.

> Anotar tudo na hora, não deixe para depois o que pode fazer hoje!!


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
