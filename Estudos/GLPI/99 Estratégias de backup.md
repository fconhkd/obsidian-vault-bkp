eni## Introdução

Fazer backup do sistema GLPI é crucial para garantir a segurança e a integridade dos dados. O GLPI é uma ferramenta de gestão de TI que armazena informações valiosas sobre ativos, tickets, usuários e muito mais. Sem backups regulares, há um risco significativo de perda de dados devido a falhas no sistema, ataques cibernéticos ou erros humanos. Manter backups atualizados permite a recuperação rápida e eficiente dos dados, minimizando o tempo de inatividade e garantindo a continuidade das operações. Além disso, os backups ajudam a cumprir requisitos de conformidade e auditoria, proporcionando uma camada adicional de segurança e tranquilidade para a organização.

## O que devo fazer backup?

Aqui estão os itens importantes que você deve incluir no backup do sistema GLPI:

1. **Banco de dados**: Contém todas as informações críticas, como tickets, ativos, usuários, configurações e histórico de atividades.
2. **Arquivos de configuração**: Incluem as configurações personalizadas do GLPI, como `config_db.php` e outros arquivos de configuração.
3. **Diretório de documentos**: Armazena anexos, documentos e outros arquivos carregados no sistema.
4. **Plugins**: Incluem todos os plugins instalados e suas configurações específicas.
5. **Logs**: Arquivos de log que podem ser úteis para auditoria e solução de problemas.
6. **Scripts personalizados**: Qualquer script ou automação personalizada que tenha sido adicionada ao sistema.

Manter esses itens sempre atualizados e seguros em seus backups garantirá que você possa restaurar o sistema GLPI de forma eficiente em caso de necessidade.
## Backups no Amazon Bucket S3

Uma das estratégias que tenho pensando em utilizar no backup do #GLPI é compactar os arquivos e envia-los a um bucket #AWS 

### Configurar bucket S3 da AWS

Para configurar um bucket S3 da AWS para apagar arquivos com mais de 45 dias, você pode usar uma regra de ciclo de vida. Aqui estão os passos para fazer isso:

1. **Acesse o console do Amazon S3**:    
    - Faça [login](https://us-east-1.console.aws.amazon.com/s) no AWS Management Console e abra o console do Amazon S3.
        
2. **Selecione o bucket**:    
    - Na lista de buckets, escolha o bucket que você deseja configurar.
        
3. **Crie uma regra de ciclo de vida**:    
    - Vá para a guia "Gerenciamento" e selecione "Criar regra de ciclo de vida".        
    - Dê um nome para a regra.
        
4. **Defina o escopo da regra**:    
    - Escolha "Aplicar a todos os objetos do bucket" ou defina um filtro específico se desejar aplicar a regra apenas a um subconjunto de objetos.
        
5. **Configure as ações da regra**:    
    - Selecione "Expirar versões atuais de objetos" e insira "45" no campo "Dias após a criação do objeto".
    - Selecione "Excluir permanentemente versões não atuais de objetos" e insira "45" no campo "Dias após os objetos se tornarem não atuais".
        
6. **Finalize a regra**:    
    - Selecione "Criar regra".
        

O Amazon S3 executa regras de ciclo de vida uma vez por dia. Depois da primeira execução, todos os objetos qualificados para expiração são marcados para exclusão.

Se precisar de mais detalhes, você pode conferir a documentação oficial da AWS [aqui](https://repost.aws/pt/knowledge-center/s3-empty-bucket-lifecycle-rule).

### Scripts de exemplo

#### Backup do banco-de-dados #MySQL

``` bash
#!/bin/bash
USER="root"
PASSWORD=""
DATA=`date +%Y/%m/%d`
DATAHORA=`date +%Y%m%d_%H%M`
OUTPUT="/backup/db/$DATA"

#Cria pastas par armazenar os backups
mkdir -p $OUTPUT

rm "$OUTPUT/*gz" > /dev/null 2>&1

#Recebe a lista de bancos a serem backupeados
databases=`mysql --user=$USER --password=$PASSWORD -e "SHOW DATABASES;" | tr -d "| " | grep -v Database`

#Faz backup das bases de dados MySql
for db in $databases; do
    if [[ "$db" != "information_schema" ]] && [[ "$db" != _* ]] ; then
        echo "Dumping database: $db"
        mysqldump --force --opt --routines --user=$USER --password=$PASSWORD --databases $db > $OUTPUT/$DATAHORA.$db.sql
        gzip $OUTPUT/$DATAHORA.$db.sql
    fi
done
```

#### Enviar arquivos ao bucket

[[Agendar]] o script no crontab do servidor

##### Banco-de-dados

``` bash
aws s3 sync /backup/database/$(date +\%Y)/$(date +\%m)/$(date +\%d) s3://bkp-glpi/database/$(date +\%Y)/$(date +\%m)/$(date +\%d)
```

##### Arquivos de configuração

``` bash
aws s3 sync /etc/glpi/ s3://bkp-glpi/config
```

##### Diretório de documentos

``` bash
aws s3 sync /var/lib/glpi s3://bkp-glpi/files
```

#### Exemplos de crontab

Um exemplo das tarefas agendadas em um servidor Linux

``` crontab
# m h  dom mon dow   command
30 23 * * * aws s3 sync /backup/db/$(date +\%Y)/$(date +\%m)/$(date +\%d) s3://bkp-glpi/db/$(date +\%Y)/$(date +\%m)/$(date +\%d)
35 23 * * * aws s3 sync /etc/glpi/ s3://bkp-glpi/config
35 23 * * * aws s3 sync /var/lib/glpi/ s3://bkp-glpi/files/
# com acesso ao db
00 23 * * * bash /etc/glpi/bkp-db-glpi.sh
```
