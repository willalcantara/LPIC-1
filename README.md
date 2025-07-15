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

---

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
- Update-grub –version , verifica a versão do grub.
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

- Apt-get -d ou –download-only install nome do pacote
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

#### 102.5 Gerenciamento de Pacotes RPM e Yum

- RPM , equivalente ao DPKG.
- O RPM trabalha em modos, existem os de consulta, instalação e remoção. Existe um de verificação, mas é pouco usado.
- Rpm -qa – mostra todos os pacotes instalados na maquina.
- Rpm -qa bash, mostra tudo de informação referente ao bash
- Rpm -qi bash, mostra detalhes sobre a instalação do bash
- Rpm -ql bash, lista os arquivos que pertence a esta instalação.
- Rpm -c , configuração
- Rpm -d, documentação
- Rpm -qf /etc/skell…/.bashrc, mostra a aplicação que instalou o arquivo.
- Rpm -qlp pacote, lista a s informações do pacote.
- Rpm -qip, lista as informações que vão ser instalada por este pacote.
- Rpm -i, instala o pacote.
- Rpm -U, realiza o update.
- Rpm -ivh, verbose e hash para mostrar o progresso.
  - O RPM não faz a resolução de dependência.
- Rpm -ivh --nodeps , ignora as dependências. Não sobrescreve o arquivo.
- Rpm -ivh –- force, ignora tudo e sobrescreve.
- Rpm -ivh –-teste, testa a instalação, mas não instala.
- Rpm -e nomedopacote. Realiza o Erase, ou seja, desinstala.
- Rpm -evh, realiza a desinstalação e mostra na tela.
- Rpm -V nomedopacote. Verifica se tem algum erro na instalação.
- Rpm -qpR ou --requires bash – mostra o que é necessário(dependências) para que o pacote seja instalado

- YUM – equivalente ao apt-get. Realiza todo o download e verificação das dependências.
- Cat /etc/yum.conf . Neste arquivo tem as principais configurações do YUM.
- Cat /etc/yum.repos.d. Neste arquivo possui os repositórios de instalação (fontes).
- Yum –help | more, mostra as varias opções de instalação.
- Yum install gcc – realiza a instalação.
- Yum update, atualiza todos os pacotes.(update –obsolate)
- Yum upgrade, remove pacotes obsoletos.
- Yum check-update, verifica se tem updates.
- yum list, lista aplicações e versões instalados. Anaconda é o que faz a instalação do S.O.
- yum search samba, pesquisa os pacotes relacionados ao samba.
- yum esta substituído pelo DNF, na distribuição fedora.
- Yum install –downloadonly nomedopacote, realiza somente o download do samba.
- ==downloaddir /tmp/samba.
- Yumdownloadernomedopacote, também realiza somente o download do pacote sh.

- Rpm –checksig, verifica se o pacote esta integro, ou seja, da mesma forma que foi gerado.
- Rpm2cpio. Transforma o RPM em um CPIO(arquivo de agrupamento).
- Rpm2cpio nomedopacote > nomedoarquivo.cpio.

---

Principais opções
Comando rpm

- -i = Instala um pacote. Normalmente utilizado com -ivh
- -U = Atualiza ou instala um pacote. Também normalmente utilizado com -Uvh
- -F = Atualiza um pacote apenas se ele já estiver instalado.
- -e = Remove um pacote
- -qa = Consulta todos os pacotes instalados
- -qi = Consulta um pacote específico
- -ql = Lista todos os arquivos de um pacote
- -qf = Indica o pacote relacionado a determinado arquivo
- -qp = Analisa um pacote .rpm não instalado (-qlp, -qip)
- -V = Verifica a integridade de um pacote
- --force = permite a substituição de arquivos existentes.
- --nodeps = não verifica dependências.
- --test = não instala efetivamente

- Comando yum
- /etc/yum.conf : principal arquivo de configuração
- /etc/yum.repos.d/ : contém os fontes de pacotes
- Check : verifica se a base de dados esta funcionando
- install = Instala um ou mais pacotes
- update = Atualiza um ou todos os pacotes
- upgrade = Atualiza um ou todos os pacotes, inclusive removendo ou substituindo pacotes obsoletos
- check-update = Verifica as atualizações de pacotes disponíveis
- list = Lista os pacotes instalados ou disponíveis
- search = Procura por um pacote baseado em uma palavra/string
- remove/erase = Remove um ou mais pacotes

- yum install –downloadonly pacote: faz o download com suas dependências mas não instala.
- Rpm –checksig : verifica a assinatura do pacote
- Rpmtocpio: transforma em cpio o arquivo rpm

- DNF – Desenvolvido a partir do Yum, melhor desempenho e resolve problemas de resolução.
- Zypper (suse): o Suse também usa pacotes RPM, porém com o comando Zipper
- Zypper repôs : mostra os repositórios configurados
- /etc/zyppe/repôs.d : diretório onde fica os repositórios do zypper.
- Zypper search calculator: pesquisa quais pacotes podem me atender.
- Zypper install zsn: instala o pacote
- Zypper refresh: atualiza os repositórios

#### 102.6 Linux and virtualization guest

![](img/img0010.png)

- O Container Engine separa as aplicações e utiliza as chamadas do S.O., no entanto com as libs separadas.
- Docker e LXC/LXD (Linux Container, foi o 1º)
- Guest Driver ou Device Drivers : Softwares, conjunto de bibliotecas e driver que permite o Guest trabalhar melhor, melhor performance
- Tipos de virtualização:
- Virtualização completa(HVM):
- A vm não sabe que ela é uma vm.
- Não é necessário modificar o S.O. do Guest
- Requer suporte da CPU
- Paravirtualização(PV):
- Modifica o S.O. do guest, o S.O. sabe que ele é o uma VM.
- Não requer suporte da CPU.
- Usto de paravirtual Drivr. Exemplo: VirtIO(KVM),Xen
- O Guest interage com o HyperVisor.

- A imagem é mais utilizada agora para container, é uma definição estática do que será o container após a inicialização.
- Pode incluir o S.O., os softares, bibliotecas, aplicações e etc.
- Fotografia do ambiente
- Cloud-init : Permite a customização de uma imagem já pronta, obtida de outras formas.
- D-BUS MACHINE ID: Identificar único de um container ou maquina virtual.
- /etc/machine-id
- Systemd-machine-id-setup –print

- Ssh host key: chave privada usada para utilizar o sistema
- Ssh -i chave.pem user@dominioouip.

- Cat qproc/cpuinfo |grep hypervisor : se não mostrar nada é uma maquina real, senão é virtual
- Demesg | grep hypervisor:
- Virt-what:
- Dmidecote -t system
- Lshw -class systemshw -class system
- Hostnamectl -status
- Systemd-detect-virt

- Systemctl start Docker
- Docker os – lista containers
- Docker run -ti centos : olha se tem o centos local, senão baixa da internet
- O container não vem com o kernel, ele usa o kernel do host.

### 104 Dispositivos, Sistemas de arquivos Linux e FHS

#### 104.1 Criando partições e sistemas de arquivos

- Fdisk -l : lista as pertições
- Fdisk /dev/sdb (entra no fdisk para um determinado HD)
- Gdisk /dev/sdc(entra no Gdisk, específico para GPT)
- Como o Linux vai trabalhar os dados e distribuir os dados, verificação de erros, tamanho de blocos e etc.

![](img/img0011.png)

- MKFS -t ext3 /dev/sdb1, faz o file system, sistemas de arquivos.
- File -s /dev/sdb1, exibe o formato da partição
- mkswap /dev/sdb5, formata a partição como swap
- swapon /dev/sdb5, ativa a partição como swap

- Parted – tem mais opções que o fdisk
- #Parted /dev/sdc
- resizepart 2 4000M (parted,número da partição e novo tamanho da partição)

#### 104.2 Mantendo a Integridade de FSs - df e du
