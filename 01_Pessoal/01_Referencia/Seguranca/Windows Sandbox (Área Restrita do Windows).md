---
title: Windows Sandbox (Área Restrita do Windows)
date: 2026-04-26 12:06
url: https://learn.microsoft.com/en-us/windows/security/application-security/application-isolation/windows-sandbox/windows-sandbox-install
tags:
  - NOTES
  - WINDOWS
  - PROJECT
  - REMEMBER
aliases:
  - Como ativar e testar coisas no windows numa area restrita
---
## Introdução

Lembre-se que no Windows 10/11 Pro é possível criar um ambiente de "sandbox" para testar algumas coisas **suspeitas, como cracks, programas suspeitos e outros projetos que tenho desenvolvido.** Ao **fechar a janela o ambiente é apagado automaticamente,** tudo é esquecido e não tem nenhum contato com o PC ou área que estou usando.

## Passo a passo para ativar

1. Abra o **Menu Iniciar** e digite: **Ativar ou desativar recursos do Windows**
2. Na lista que aparecer, marque a opção: **Área Restrita do Windows**
3. Clique em **OK**.
4. Reinicie o computador quando solicitado.
5. Após reiniciar, abra o Menu Iniciar e procure por: **Windows Sandbox** ou **Área Restrita do Windows**

## Ativar o Windows Sandbox via PowerShell

1. **Abrir o PowerShell como Administrador**
	1. **Clique com o botão direito** no botão Iniciar.
	2. Escolha **Windows PowerShell (Admin)** ou **Terminal Windows (Admin)**.
	3. Confirme o controle de conta de usuário (UAC), se aparecer.
2. **Executar o comando para habilitar o recurso**
	1. Copie e cole este comando na janela do PowerShell elevada e pressione **Enter**:
		```powershell
	Enable-WindowsOptionalFeature -FeatureName "Containers-DisposableClientVM" -All -Online
		```
3. Reiniciar o computador
	1. Quando o PowerShell pedir para reiniciar, digite **Y** e pressione **Enter** ou reinicie manualmente depois que o comando terminar.
4. Abrir o Windows Sandbox
	1. Após o reboot, abra o **Menu Iniciar** e procure por: **Área Restrita do Windows**
	2. É ali que o _Windows Sandbox_ vai aparecer no sistema em PT‑BR.


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
