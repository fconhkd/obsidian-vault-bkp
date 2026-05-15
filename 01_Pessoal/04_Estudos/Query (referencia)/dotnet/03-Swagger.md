---
title: 03-Swagger
date: 2026-01-18 20:33
url: https://learn.microsoft.com/pt-br/aspnet/core/tutorials/getting-started-with-swashbuckle?view=aspnetcore-8.0&tabs=visual-studio
tags:
  - DEVELOPER
  - DOTNET
  - OPENAPI
  - SWAGGER
aliases:
---
## Introdução

No .NET 9 e posterior, o ASP.NET Core inclui suporte interno ao OpenAPI. O Swashbuckle não está mais incluído por padrão, mas ele permanece disponível como um pacote de comunidade que você pode adicionar manualmente aos projetos do ASP.NET Core direcionados ao .NET 9 ou posterior.

## Instalação do Pacote

Execute o seguinte comando:
```bash
dotnet add TodoApi.csproj package Swashbuckle.AspNetCore -v 6.6.2
```
## Adicionar e configurar o middleware do Swagger

Adicione o gerador do Swagger à coleção de serviços no `Program.cs`:
```C#
builder.Services.AddControllers();

builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();
```
A chamada a [AddEndpointsApiExplorer](https://learn.microsoft.com/pt-br/dotnet/api/microsoft.extensions.dependencyinjection.endpointmetadataapiexplorerservicecollectionextensions.addendpointsapiexplorer) mostrada no exemplo anterior é necessária apenas para [Minimal APIs](https://learn.microsoft.com/pt-br/aspnet/core/fundamentals/apis). Para obter mais informações, confira [este post do StackOverflow](https://stackoverflow.com/a/71933535).

Habilite o middleware para servir o documento JSON gerado e a interface do usuário do Swagger, também em `Program.cs`:
```C#
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}
```
O código anterior adiciona o middleware swagger somente se o ambiente atual estiver definido como `Development`. A chamada do método `UseSwaggerUI` habilita uma versão incorporada da interface Swagger.

Inicie o aplicativo e navegue até `https://localhost:<port>/swagger/v1/swagger.json`. O documento gerado que descreve os pontos de extremidade é exibido conforme mostrado na [Especificação do Openapi (openapi.json)](https://learn.microsoft.com/pt-br/aspnet/core/tutorials/web-api-help-pages-using-swagger?view=aspnetcore-8.0#openapi-specification-openapijson).

A interface do usuário do Swagger pode ser encontrada em `https://localhost:<port>/swagger`. Explore a API por meio da interface do usuário do Swagger e incorpore-a em outros programas.

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
