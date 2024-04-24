### 102 Instalação do Linux e Gerenciamento de Pacotes

#### 102.1 Instalação do Linux e Gerenciamento de Pacotes
![](img/img006.png)

- Ponto de montagem: Pegar um diretório e associar a uma partição
- File System: tipo do arquivo do sistema que vai de acordo com o que vai ser armazenado
- Sistemas de particionamentos (Modelos de forma de fazer o particionamento):
   - MBR – padrão limitado a 2 TB por partição
   - GPT – Utilizado na maioria dos sistemas com EFI, aceita mais que 2 TB.
   - (MBR)Partições primarias são numeradas de 1 a 4, sda1,sda2,sda3,sd4
   - (MBR)Partições estendidas são numeradas a partir de 5, sda5,sd6 e etc.
- Códigos dos tipos de partição
   - 0x83 – Linux FilesSystem
   - 0x82 – Linux Swap
- Partições Comuns
- /home – dados dos usuários (Separar para que não afete a aplicação)
- /var – tem muitos arquivos temporários e filas, exemplos filas de e-mail
- /tmp – tem muitos arquivos temporários e de lock
- /boot – arquivos do kernel e initrd. Em sistemas antigos, o gerenciador de boot só conseguir acessar os dados no limite do cilindro 1024 do disco e por isso era comum se criar esta partição. Para garantir que esteja antes do cilindro 1024, partição pequena, geralmente com 50 MB.
- /usr – Possui muitas aplicações instaladas.
----------------------------------------------
- Diretórios que não podem ser montados fora do Barra
- /etc – maioria dos arquivos de configuração do sistema
- /bin – fica os comandos, scripts e programas utilizados no Linux
- /sbin – fica os comandos, scripts e programas
- /dev
- /proc
- /sys

- LVM – Forma de gerenciamento Lógico
- Maior facilidade de redirecionamento
![](img/img0007.png)
- VG: Volume group
- PV: Phisical volume
- LV: Logical Volume
- PE: Physical Extend
- LE: Logical Extend
- Cat /procs/swaps – vejo as partições swaps
- Df -T , verifique a partição do tipo VFAT, esta montada no /boot/efi
- Efibootmgr : ver informações e fazer alterações no EFI

#### 102.2 Instalação do boot manager
Exitem 2 grubs, o Grub Legacy e o Grub2.
![](img/img0008.png)

Cd / boot
#Você irá ver as várias imagens de Kernel, o initrd e outros como o teste de memória.
Cd /boot/grub
 Update-grub –version , verifica a versão do grub.
O padrão é alterar os parâmetros do /etc/default/grub
Grub-mkconfig -o /boot/grub/grub.cfg
Update-grub
Fazer backup do bootloader(grub)
Dd if=/dev/sda of=copia.mbr bs=1 count=512, realizando cópia do disco
