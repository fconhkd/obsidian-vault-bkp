---
title: Hardening de Headers de Segurança
date: 2025-12-24 13:50
url: https://securityheaders.com/
tags:
  - CYBERSECURITY
  - DEFENSIVE
  - NGINX
  - WORDPRESS
  - PCI-DSS
  - CIS
  - SECURITY-HEADERS
aliases:
  - Aplicação de Headers de Segurança HTTP
---
## Introdução

Este documento descreve **as etapas e configurações recomendadas de headers HTTP de segurança** para aplicações web em geral (sites institucionais, portais e aplicações tradicionais), utilizando **servidores web modernos** (como Nginx, Apache ou equivalentes).

O objetivo é:

- Reduzir a superfície de ataque    
- Aplicar boas práticas de hardening    
- Atender requisitos comuns de **CIS Benchmarks**, **OWASP** e **PCI DSS v4.0**    
- Servir como material de referência técnica e auditoria

## 1. Pré-requisitos

- Servidor web (Nginx, Apache ou compatível)    
- Aplicação web funcional    
- Permissão administrativa para alterar a configuração do servidor    
- Conhecimento básico de configuração HTTP

## 2. Onde aplicar os headers

Os headers HTTP de segurança devem ser aplicados **no nível do servidor web**, garantindo que todas as respostas HTTP incluam as diretivas configuradas.

### Locais comuns de aplicação

- Bloco de **virtual host / server**    
- Contexto global do servidor (`http` ou `server`)    
- Arquivo incluído especificamente para headers de segurança

> **Boa prática:** aplicar no menor escopo possível que cubra toda a aplicação.

---

## 3. Headers de Segurança Recomendados

### 3.1 X-Frame-Options (Proteção contra Clickjacking)

```bash
add_header X-Frame-Options "SAMEORIGIN" always;
```

**Motivo:**

- Impede que o site seja carregado em iframe por terceiros    
- Permite uso interno (mesmo domínio)    

---

### 3.2 Content-Security-Policy (Frame Ancestors)

```bash
add_header Content-Security-Policy "frame-ancestors 'self'" always;
```

**Observação:**

- Este é o **substituto moderno** do X-Frame-Options    
- Compatível com navegadores modernos    

---

### 3.3 X-Content-Type-Options

```bash
add_header X-Content-Type-Options "nosniff" always;
```

**Motivo:**

- Evita execução de arquivos com MIME incorreto    
- Reduz risco de XSS baseado em tipo de conteúdo    

---

### 3.4 Referrer-Policy

```bash
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
```

**Motivo:**

- Evita vazamento de URLs completas    
- Mantém compatibilidade com analytics    

---

### 3.5 Permissions-Policy (Perfil Institucional Genérico)

> Configuração equilibrada: segura sem quebrar plugins comuns

```bash
add_header Permissions-Policy "accelerometer=(), autoplay=(), camera=(), clipboard-read=(), clipboard-write=(self), display-capture=(), encrypted-media=(), fullscreen=(self), geolocation=(), gyroscope=(), magnetometer=(), microphone=(), midi=(), payment=(), picture-in-picture=(), publickey-credentials-get=(), usb=(), screen-wake-lock=(), web-share=()" always;
```

**Principais decisões:**

- `fullscreen=(self)` → vídeos em tela cheia    
- `clipboard-write=(self)` → formulários e UX    
- APIs sensíveis desabilitadas    

---

### 3.6 Strict-Transport-Security (HSTS)

> ⚠️ Aplique **somente se HTTPS estiver 100% funcional**

```bash
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
```

**Motivo:**

- Força HTTPS    
- Previne SSL stripping    

---

## 4. Configuração Final (Combo Completo)

```bash
add_header X-Frame-Options "SAMEORIGIN" always;
add_header Content-Security-Policy "frame-ancestors 'self'" always;
add_header X-Content-Type-Options "nosniff" always;
add_header Referrer-Policy "strict-origin-when-cross-origin" always;
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
add_header Permissions-Policy "accelerometer=(), autoplay=(), camera=(), clipboard-read=(), clipboard-write=(self), display-capture=(), encrypted-media=(), fullscreen=(self), geolocation=(), gyroscope=(), magnetometer=(), microphone=(), midi=(), payment=(), picture-in-picture=(), publickey-credentials-get=(), usb=(), screen-wake-lock=(), web-share=()" always;
```

---

## 5. Testes e Validação

### 5.1 Teste via linha de comando

```bash
curl -I https://seudominio.com
```

Verifique a presença de todos os headers.

### 5.2 Ferramentas Online

- Security Headers    
- Mozilla Observatory    

---

## 6. Ajustes Comuns

|Cenário|Ajuste Necessário|
|---|---|
|Mapa com geolocalização|Liberar `geolocation=(self)`|
|WebAuthn / Passkeys|Liberar `publickey-credentials-get=(self)`|
|Site embedado em outro domínio|Ajustar `frame-ancestors`|

---

## 7. Boas Práticas Operacionais

- Versionar todas as alterações de configuração    
- Testar os headers em ambiente de homologação antes de produção    
- Monitorar erros no console do navegador após a aplicação    
- Revisar headers periodicamente ou após mudanças relevantes na aplicação    
- Evitar exceções amplas (ex: `*` ou domínios genéricos)    

---

## 8. Referências de Compliance

- PCI DSS v4.0 – Requirement 6
- CIS Controls – Secure Configuration
- OWASP Secure Headers Project

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
