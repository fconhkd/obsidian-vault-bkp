---
title: Procedimento de Instalação do GLPI
date: 2025-10-23T23:59:00
tags:
  - GLPI
  - ITSM
---

> Em 1 de Outubro de 2025, foi liberada pela Teclib a nova versão do GLPi, a versão 11.

## Pré-requisitos

Aprenda de forma rápida e direta a instalar o GLPi 10 e já partir para o gerenciamento de serviços no seu ambiente, se você precisa atualizar [clique aqui](Atualizando%20o%20GLPI.md).

### Atualizando a lista de pacotes disponíveis

Nosso primeiro passo será atualizar a lista de pacotes disponíveis nos repositórios configurados no GNU/Linux Debian.

``` bash linenums="1" title=""
# Atualiza Lista de Pacotes
apt update
```

### Fuso horário

O GLPi finalmente traz a possibilidade de podermos trabalhar com diferentes fusos na Central de Serviços. Aqui vão alguns comandos de ajuste geral para isso:

``` Bash linenums="1"
# Configurar Timezone padrão do Servidor
dpkg-reconfigure tzdata
```

``` Bash linenums="1"
# Adicionar servidor NTP.BR
echo "NTP=pool.ntp.br" >> /etc/systemd/timesyncd.conf
echo "FallbackNTP=pool.ntp.br" >> /etc/systemd/timesyncd.conf
```

``` Bash linenums="1"
# Habilitar e Iniciar Serviço OpenNTPD
systemctl enable systemd-timedated.service
systemctl start systemd-timedated.service
```

### Pacotes para Manipulação de Arquivos

Se você tiver realizado uma instalação minimalista do sistema operacional, tal como sempre recomendamos, é provável que você precise de um pouco mais de ferramentas para manipulação de arquivos, consumir API dentre outras coisas.

Os comandos abaixo lhe auxiliarão com isso:

``` Bash linenums="1"
# PACOTES MANIPULAÇÃO DE ARQUIVOS
apt install -y xz-utils bzip2 unzip curl
```

## Preparação do Servidor WEB

Como já sabemos, o GLPi trata-se de uma ferramenta WEB. Podemos vê-lo simplesmente como um site a ser instalado. Portanto, precisamos montar um ambiente WEB para tal funcionalidade.

Existem várias opções de serviço WEB a ser utilizada em ambientes GNU/Linux. Utilizaremos o servidor WEB Apache.

Para habilitar o serviço Apache em seu servidor, basta seguir o comando abaixo:
``` Bash linenums="1"
# Instalar dependências no sistema
apt install -y apache2 libapache2-mod-php php-soap php-cas php php-{apcu,cli,common,curl,gd,imap,ldap,mysql,xmlrpc,xml,mbstring,bcmath,intl,zip,redis,bz2}
```

O GLPi é um sistema desenvolvido na linguagem PHP, por isso, neste comando instalamos vários módulos PHP.

Ao fim deste comando, teremos um servidor WEB instalado já com suporte a linguagem PHP e com todas as dependências do GLPi resolvidas.

## Resolvendo Problema de Acesso WEB ao Diretório

Um ajuste que muitos deixam de fazer é com relação a permissão de acesso ao diretório WEB. Isso pode ser resolvido de forma simples com uma pequeno arquivo de configuração.

Para criar o arquivo e habilitar a configuração, basta executar os comandos a seguir:

``` bash linenums="1"
# Criar arquivo com conteúdo
cat > /etc/apache2/conf-available/glpi.conf << EOF
<Directory "/var/www/html/glpi/public/">
    AllowOverride All
    RewriteEngine On
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule ^(.*)$ index.php [QSA,L]
    Options -Indexes
    Options -Includes -ExecCGI
    Require all granted
    <IfModule mod_php7.c>
        php_value max_execution_time 600
        php_value always_populate_raw_post_data -1
    </IfModule>
    <IfModule mod_php8.c>
        php_value max_execution_time 600
        php_value always_populate_raw_post_data -1
    </IfModule>
</Directory>
EOF
# Habilitar o módulo rewrite do apache
a2enmod rewrite
# Habilita a configuração criada
a2enconf glpi.conf
# Reinicia o servidor web considerando a nova configuração
systemctl restart apache2
```

## Baixar e Instalar o GLPi

Por comodidade, colocaremos o GLPi na pasta padrão do Apache, lembrando que isso não é uma regra.

Repare que fizemos tudo com apenas 1 linha de comando para você, de forma que fique bem simples:

``` bash linenums="1"
# Criar os diretórios do GLPi
mkdir /var/www/html/glpi/
mkdir /var/lib/glpi/
mkdir /var/log/glpi/
mkdir /etc/glpi/
```

``` bash linenums="1"
# Baixar o sistema GLPi
wget -O- https://github.com/glpi-project/glpi/releases/download/11.0.6/glpi-11.0.6.tgz | tar -zxv -C /var/www/html/
```

``` bash linenums="1"
# Movendo diretórios "files" e "config" para fora do GLPi 
mv /var/www/html/glpi/files /var/lib/glpi/
mv /var/www/html/glpi/config /etc/glpi/
```

``` bash linenums="1"
# criar o arquivo inc/downstream.php
cat << 'EOF' > /var/www/html/glpi/inc/downstream.php
<?php
define('GLPI_CONFIG_DIR', '/etc/glpi/');

if (file_exists(GLPI_CONFIG_DIR . '/local_define.php')) {
   require_once GLPI_CONFIG_DIR . '/local_define.php';
}
EOF
```

```bash
# criando o arquivo de configuração
cat << 'EOF' > /etc/glpi/local_define.php
<?php
define('GLPI_VAR_DIR', '/var/lib/glpi');
define('GLPI_DOC_DIR',        GLPI_VAR_DIR);                  // Path for documents storage
define('GLPI_CACHE_DIR',      GLPI_VAR_DIR . '/_cache');      // Path for cache storage
define('GLPI_CRON_DIR',       GLPI_VAR_DIR . '/_cron');       // Path for cron storage
define('GLPI_GRAPH_DIR',      GLPI_VAR_DIR . '/_graphs');     // Path for graph storage
define('GLPI_LOCAL_I18N_DIR', GLPI_VAR_DIR . '/_locales');    // Path for local i18n files
define('GLPI_LOCK_DIR',       GLPI_VAR_DIR . '/_lock');       // Path for lock files storage (used by cron)
define('GLPI_LOG_DIR',        GLPI_VAR_DIR . '/_log');        // Path for log storage
define('GLPI_PICTURE_DIR',    GLPI_VAR_DIR . '/_pictures');   // Path for picture storage
define('GLPI_PLUGIN_DOC_DIR', GLPI_VAR_DIR . '/_plugins');    // Path for plugins documents storage
define('GLPI_RSS_DIR',        GLPI_VAR_DIR . '/_rss');        // Path for RSS feeds storage
define('GLPI_SESSION_DIR',    GLPI_VAR_DIR . '/_sessions');   // Path for sessions files storage
define('GLPI_TMP_DIR',        GLPI_VAR_DIR . '/_tmp');        // Path for temporary files storage
define('GLPI_UPLOAD_DIR',     GLPI_VAR_DIR . '/_uploads');    // Path for upload storage
define('GLPI_INVENTORY_DIR',  GLPI_VAR_DIR . '/_inventories');// Path for inventory files storage
define('GLPI_THEMES_DIR',     GLPI_VAR_DIR . '/_themes');     // Path for custom themes storage
define('GLPI_MARKETPLACE_DIR', '/var/lib/glpi/plugins');	
EOF
```
## Ajustar Permissões de Arquivos

Com os arquivos já em seu devido lugar, faremos agora um ajuste em cima das permissões destes. Execute os seguintes comando:

``` bash linenums="1"
# Ajustar propriedade de arquivos da aplicação GLPi
chown www-data:www-data /var/www/html/glpi -Rf
find /var/www/html/glpi/ -type d -exec chmod 755 {} \;
find /var/www/html/glpi/ -type f -exec chmod 644 {} \;

chown www-data:www-data /var/lib/glpi -Rf
sudo find /var/lib/glpi -type d -exec chmod 755 {} \;
sudo find /var/lib/glpi -type f -exec chmod 644 {} \;

chown www-data:www-data /etc/glpi -Rf
sudo find /etc/glpi -type d -exec chmod 755 {} \;
sudo find /etc/glpi -type f -exec chmod 644 {} \;
```

## Configurando o apache

Primeiro de tudo temos que desabilitar o site padrão e criar o arquivo de configuração para o site glpi no apache

```bash
# Desabilitando site padrão do Apache
a2dissite 000-default.conf
```

```bash
# criar um arquivo de configuração do site glpi
cat > /etc/apache2/sites-available/glpi.conf << EOF
<VirtualHost *:80>
        #ServerName suporte.empresa.NET.br
        ServerAdmin suporte@empresa.com.br
        DocumentRoot /var/www/html/glpi/public

        ErrorLog ${APACHE_LOG_DIR}/glpi.error.log
        CustomLog ${APACHE_LOG_DIR}/glpi.access.log combined
</VirtualHost>
EOF
# Habilita o site criada
a2ensite glpi.conf
# Reinicia o servidor web 
systemctl restart apache2
```

## Instalando o MySQL

```bash
# Instalando o Serviço MySQL
apt install -y mariadb-server
```

Ao fim deste comando teremos já um serviço MySQL disponível para ser utilizado em nosso Servidor.
## Criando Usuário e Base de Dados MySQL

Apesar de termos nosso Serviço SQL rodando, ainda precisamos criar uma base de dados a ser utilizada pelo sistema e uma conta de acesso administrativo a essa base, também a ser utilizada pelo sistema GLPi.

Para tanto, basta usar os comandos abaixo:

```bash
# Criando base de dados
mysql -e "create database glpi character set utf8"
# Criando usuário
mysql -e "create user 'glpi'@'localhost' identified by '123@456#'"
# Dando privilégios ao usuário
mysql -e "grant all privileges on glpi.* to 'glpi'@'localhost' with grant option";
```


```bash
# Habilitando suporte ao timezone no MySQL/Mariadb
mysql_tzinfo_to_sql /usr/share/zoneinfo | mysql mysql
# Permitindo acesso do usuário ao TimeZone
mysql -e "GRANT SELECT ON mysql.time_zone_name TO 'glpi'@'localhost';"
# Forçando aplicação dos privilégios
mysql -e "FLUSH PRIVILEGES;"
```



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
