---
title: Procedimento de atualização do GLPI
date: 2025-10-23T23:59:00
tags:
  - GLPI
  - ITSM
---
## Introdução

> Fique atento aos lançamentos de versão do projeto GLPI, acesse o projeto nesse link [https://github.com/glpi-project/glpi/releases/latest](https://github.com/glpi-project/glpi/releases/latest)

### Fazer backup do sistema

Como para cada processo de atualização, você precisa fazer backup de alguns dados antes de processar qualquer atualização:

- Faça backup do banco de dados;
- Faça backup do diretório config, especialmente para o arquivo de chave GLPI (config/glpi.key ou config/glpicrypt.key) que é gerado aleatoriamente;
- Faça backup do diretório de arquivos, ele contém usuários e plugins gerados arquivos, como documentos carregados;
- Faça backup do seu diretório de marketplace e plugins.

``` bash linenums="1"
# executar o script de backup
bash /backup/script-bkp-glpi.sh
```

### Baixando e Instalando a ultima versão

Acesse o [link](https://github.com/glpi-project/glpi/releases/latest), copie o link para a ultima versão do arquivo e execute o comando abaixo.

``` bash linenums="1"
# baixar com wget a ultima versão
wget https://github.com/glpi-project/glpi/releases/download/10.0.20/glpi-10.0.20.tgz
```

``` bash linenums="3"
# parar o serviço do apache
service apache2 stop
```

``` bash linenums="5"
# renomear a pasta do glpi
mv /var/www/html/glpi /var/www/html/glpi-old
```

``` bash linenums="7"
#descompactar a nova versão em cima da atual
tar zxfv /var/www/html/glpi-10.0.20.tgz
```

``` bash linenums="9"
#copie o arquivo de inc/downstream.php
cp /var/www/html/glpi-old/inc/downstream.php /var/www/html/glpi/inc/
```

``` bash linenums="11"
# copiando a pasta de plugins
cp -r /var/www/html/glpi-old/plugins/* /var/www/html/glpi/plugins/

# copiando a pasta marketplace
cp -r /var/www/html/glpi-old/marketplace/* /var/www/html/glpi/marketplace/

# copiando imagens
cp -r /var/www/html/glpi-old/pics/logos/* /var/www/html/glpi/pics/logos/
```

``` bash linenums="19"
#ajustar permissões da pasta nova
chown www-data:www-data /var/www/html/glpi -Rf
find /var/www/html/glpi -type d -exec chmod 755 {} \;
find /var/www/html/glpi -type f -exec chmod 644 {} \;
```

``` bash linenums="23"
#atualizar o banco-de-dados do glpi
php /var/www/html/glpi/bin/console db:update
```

Agora ligue o serviço do apache e teste a versão nova, acesse o sistema via browser.

``` bash linenums="1"
#apagar a pasta de instalação
rm -r /var/www/html/glpi/install

#ligando o serviço do apache
service apache2 start
```

Se tudo deu certo seu glpi foi atualizado para a ultima versão, acesse a pagina de configuração para ver os detalhes.


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
