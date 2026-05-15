---
title: Introdução aos Diagramas Mermaid
date: 2026-01-17 18:15
url: https://mermaid.js.org/
tags:
  - OBSIDIAN
  - REMEMBER
  - NOTES
aliases:
  - diagramas no obsidian
---
## Introdução

Gosto de usar Mermaid no Obsidian porque ele me permite transformar ideias em desenhos simples e rápidos sem sair do Markdown. Sempre que preciso visualizar um processo, organizar um fluxo ou entender melhor uma estrutura, crio um diagrama aqui mesmo. Esta página é meu espaço de referência para lembrar como escrever cada tipo de diagrama e ter exemplos prontos para copiar quando precisar.

## 🟦 1. Criar um bloco Mermaid

Basta abrir um bloco de código com `mermaid`:

markdown

````
```mermaid
graph TD
    A[Início] --> B[Processar ideia]
    B --> C{É útil?}
    C -->|Sim| D[Virar nota]
    C -->|Não| E[Arquivar]
```
````

Quando você fecha o bloco, o Obsidian renderiza automaticamente o diagrama.

## 🟦 2. Tipos de diagramas que você pode criar

### 🔹 Fluxogramas (graph)

markdown

````
```mermaid
graph LR
    A --> B
    B --> C
```
````

### 🔹 Diagramas de sequência

markdown

````
```mermaid
sequenceDiagram
    Alice->>Bob: Olá
    Bob-->>Alice: Oi
```
````

### 🔹 Diagramas de classe

markdown

````
```mermaid
classDiagram
    Animal <|-- Cachorro
    Animal <|-- Gato
```
````

### 🔹 Diagramas de Gantt (cronogramas)

markdown

````
```mermaid
gantt
    title Projeto X
    section Planejamento
    Tarefa A :a1, 2026-01-17, 3d
    Tarefa B :after a1, 5d
```
````

### 🔹 Diagramas de estado

markdown

````
```mermaid
stateDiagram
    [*] --> Ideia
    Ideia --> EmProgresso
    EmProgresso --> Concluído
```
````

## 🟦 3. Ativar suporte ao Mermaid (se não estiver funcionando)

Normalmente já vem ativado, mas caso não:

1. Vá em **Settings → Editor**
    
2. Ative **“Show code block preview”**
    
3. Vá em **Settings → Appearance**
    
4. Ative **“Enable Mermaid diagrams”**
    

Pronto, tudo renderiza automaticamente.

## 🟦 4. Dicas para deixar seus diagramas mais bonitos

- Use `LR` (left-to-right) ou `TD` (top-down) para controlar o fluxo
    
- Use colchetes para formas diferentes:
    
    - `A[Retângulo]`
        
    - `A(Rounded)`
        
    - `A{Decisão}`
        
    - `A((Círculo))`
        
- Use cores com `style`:
    

markdown

````
```mermaid
graph TD
    A --> B
    style A fill:#f9f,stroke:#333,stroke-width:2px
```
````

## 🟦 5. Exemplo completo para você copiar

markdown

````
```mermaid
graph TD
    A[Capturar ideia] --> B[Processar]
    B --> C{É ação?}
    C -->|Sim| D[Adicionar ao projeto]
    C -->|Não| E[Guardar em Referências]
    D --> F[Executar]
    E --> F
```
````

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
