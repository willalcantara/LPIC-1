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
- Exitem 2 grubs, o Grub Legacy e o Grub2.
![](img/img0008.png)

- Cd / boot
- #Você irá ver as várias imagens de Kernel, o initrd e outros como o teste de memória.
- Cd /boot/grub
-  Update-grub –version , verifica a versão do grub.
- O padrão é alterar os parâmetros do /etc/default/grub
- Grub-mkconfig -o /boot/grub/grub.cfg
- Update-grub
- Fazer backup do bootloader(grub)
- Dd if=/dev/sda of=copia.mbr bs=1 count=512, realizando cópia do disco

#### 102.3 Gerenciando biblioteca compartilhada
- É quando vc desenvolve um programa que usa uma referência a um bloco de código fora da sua aplicação.
- É uma forma de reuso de código.
- Ldd /usr/bin/vi, mostra todas as bibliotecas do VI. Tudo com a extensão .so.
- /lib e /usr/lib : Contém as bibliotecas usadas por outros programas.
- Ld.so.conf – contém as configurações dos diretórios onde serão procuradas as bibliotecas.
- Ldconfig : usado para recompilar o ld.so.cache.
- Ldconfig – p : lista todas as bibliotecas ativas no momento
- Caso o usuário não seja o root, ele pode incluir bibliotecas temporariamente adicionando uma variável chamada LD_LIBRARY_PATH

#### 102.4 Gerenciamento de pacotes no Debian
![](img/img0009.png)
- Dpkg -l – lista os pacotes instalados, com L maiúsculo ele lista os arquivos que está associado ao pacote
- Dpkg – bash, mostra as informações do pacote bash
- Dpkg –get-selections, faz basicamente a mesma função.
- Dpkg – contentes : mostra a lista de arquivos que tem dentro do pacote.
- Para instalar o novo pacote
  - 1 – baixar um pacote caso não tenha um repositório pessoal
  - 2 – dpkg -i Nome do pacote
- Remover o pacote
  - 1 – dpkg -r nome do pacote
- Para remover todas as informações dpkg - - purge ksh

- Apt-cache -package names, mostra a informações da base de dados dele.
- Apt-cache show vim
- Apt-cache dependes vim (quais os pacotes que o vim depende)
- Apt-get

- /etc/apt/sources.list, neste arquivo possui todas as origens de arquivos
- Apt-get update ( verifica o sources.list e atualiza as informações da base dados com base nele)
- Apt-get dist-upgrade, este pega tudo que tem na maquina e ve se tem versões mais atualizadas.
- Instalando: apt-get install zsh 
- Removendo: apt-get purge ou apt-get remove zsh zhs-common
- Apt-get check| berifica se esta tudo funcionando
- Apt-get clean, faz o house keeping, remove arquivos temporários e etc.

- Apt-get -d  ou –download-only install nome do pacote
- O arquivo irá estar no /var/cache/apt/archives.

- Dpkg-reconfigure, utiliza uma interface de configurações de pacotes.
- Exemplo: dpkg-reconfigure tzdata/keyborad-configuration

- Dselect, é uma interface gráfica do apt.
- Aptitude, faz também uma interface gráfica.

- Aptitude search csh ( procura pelo nome csh)

- Alien, converte pacotes não entendidos para instalar.
- Alien -r nomedopacote , transforma em pacote RPM
- Alien -i
- Principais Opções dos Comandos Utilizados no Gerenciamento de Pacotes Debian

- Comando dpkg
   - -i = instalar
   - -r = remover
   - -P = remover completamente
   - -I ou --contents = informações sobre um pacote não instalado. Arquivo .deb é informado no comando.
   - -l = Apenas "dpkg -l" lista todos os pacotes instalados. O nome do pacote também pode ser inserido no final do comando: "dpkg -l bash"
   - -L = Lista todos os arquivos relacionados a determinado pacote
   - -s = status de um pacote
   - -S = Informa o pacote ao qual o arquivo informado está associado. Ex: dpkg -S /etc/sudoers
   - --get-selections = Lista todos os pacotes instalados


- Comando apt-cache
- show = Mostra as informações de um pacote específico
- pkgnames = Mostra todos os pacotes instalados
- depends = Exibe informações de dependência de determinado pacote. Exemplo apt-cache depends vim

- Comando apt-get
- update = Obtém informações atualizadas das fontes
- upgrade = Realiza a atualização de todos os pacotes
- dist-upgrade = Realiza a atualização de todos os pacotes, desde que não haja quebra de dependências
- install = Instalar um pacote
- remove = Remover um pacote
- purge = Remover um pacote e todos os seus arquivos de configuração
- check = Verifica todos os pacotes em busca de quebras de dependências e inconsistências na base de dados
- apt-get –download-only install zsh : apenas faz o download do arquivo para o /var/cache/apt/archives

- dpkg-reconfigure: Permite a reconfiguração de algum pacote que exija interação.
- Dselect: interface gráfica do APT.
- Alien: converte ou instala pacotes/binários alienígenas ( não .deb), como tgz,rpm e etc.
- Alien -r package.deb : transforma pacote em .rpm
- Alien -i package.rpm

- Principais arquivos de configuração
- /etc/apt/sources.list : contém as fontes/origens de arquivos
- /etc/apt/sources.list.d/

- APT – ADVANCED PACKAGE TOOL
- Apt search calculator: procura o pacote pela descrição
- Apt list: procura pelo nome
- Apt show pacote: mosta informações
- Apt install pacote: instala o pacote
- Apt remove pacote ou apt purge pacote remove o pacote


