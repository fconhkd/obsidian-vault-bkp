---
title: Usar user-secrets no projeto dotnet
date: 2026-01-18 20:06
url: https://learn.microsoft.com/en-us/aspnet/core/security/app-secrets?view=aspnetcore-10.0&tabs=windows
tags:
  - DEVELOPER
  - DOTNET
aliases:
  - Proteger segredos no projeto
---
## Introdução

Este artigo explica como gerenciar dados sensíveis para um aplicativo .NET em uma máquina de desenvolvimento. Nunca armazene senhas ou outros dados sensíveis em código-fonte ou arquivos de configuração. Segredos de produção não devem ser usados para desenvolvimento ou teste. Segredos não devem ser implantados com o app. Os segredos de produção devem ser acessados por meios controlados, como Azure Key Vault.

## Como funciona a ferramenta Secret Manager

A ferramenta Secret Manager esconde detalhes de implementação, como onde e como os valores são armazenados. Você pode usar a ferramenta sem conhecer esses detalhes da implementação. Os valores são armazenados em um arquivo JSON na pasta de perfil de usuário da máquina local:
```path
Windows:
`%APPDATA%\Microsoft\UserSecrets\<user_secrets_id>\secrets.json`

Linux:
`~/.microsoft/usersecrets/<user_secrets_id>/secrets.json`
```
## Habilitar armazenamento secreto

A ferramenta Secret Manager opera com configurações específicas de cada projeto armazenadas no seu perfil de usuário.

```.NET Cli
dotnet user-secrets init
```

## Escondendo um segredo

Defina um segredo de aplicativo que consiste em uma chave e seu valor. O segredo está associado ao valor do projeto. Por exemplo, execute o seguinte comando a partir do diretório onde o arquivo do projeto existe:`UserSecretsId`
```
dotnet user-secrets set "Movies:ServiceApiKey" "12345"
```
A ferramenta Gerenciamento de Segredos também pode ser usada em outros diretórios. Use a opção de fornecer o caminho do sistema de arquivos onde o arquivo do projeto existe. Por exemplo:`--project`
```
dotnet user-secrets set "Movies:ServiceApiKey" "12345" --project "C:\apps\WebApp1\src\WebApp1"
```



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
