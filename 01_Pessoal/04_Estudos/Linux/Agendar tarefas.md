O `cron` é uma ferramenta poderosa no #Linux para agendar tarefas. Aqui estão os passos para agendar um comando utilizando o cron:

1. **Acesse o terminal**:    
    - Abra o terminal no seu sistema Linux.
        
2. **Edite a tabela de cron jobs**:    
    - Digite `crontab -e` no terminal para editar a tabela de cron jobs do usuário atual. Isso abrirá um editor de texto.
        
3. **Entenda a sintaxe do cron**:    
    - Cada linha na tabela de cron jobs segue a seguinte sintaxe:
			```
			* * * * * comando_a_ser_executado
			```
        - O primeiro campo representa os minutos (0-59).            
        - O segundo campo representa as horas (0-23).            
        - O terceiro campo representa o dia do mês (1-31).            
        - O quarto campo representa o mês (1-12).            
        - O quinto campo representa o dia da semana (0-7, com 0 e 7 representando domingo).            
        - O último campo é o comando a ser executado.