# Linux

Exercícios para o Tópico 102
Os exercícios a seguir tem a finalidade principal de revisar e praticar o que estudamos durante as aulas, no entanto, você também pode ser desafiado a descobrir novas opções ou formas de uso dos comandos, inclusive combinando comandos estudados em diferentes sub-tópicos.

### 102.1 Design do Layout do HD

- 1. Em sua máquina Linux, quais as partições e os respectivos pontos de montagem de cada uma delas.
- 2. Qual o tamanho de sua área de swap.
- 3. Por que diretórios como /bin, /sbin e /etc não podem ser montados fora da partição / ?
- 4. Em um sistema que utiliza UEFI, como pode ser identificada a partição em que está montado o ESP?
- 102.2 Instalação do Boot Manager (GRUB)
- 5. Qual o gerenciador de boot utilizado em sua instalação? Sendo GRUB, qual a versão?
- 6. Qual a versão do kernel que está sendo carregada por padrão em seu bootloader?
- 7. Altere os seguintes parâmetros nas configurações de seu boot loader (faça um arquivo de backup antes de alterar)?
- Mude o tempo de timeout para 15 segundos
- Inclua no título da distribuição padrão a descrição " - Curso LPI 1"
- 102.3 Gerenciamento de Bibliotecas Compartilhadas
- 8. Em sua instalação, quantas bibliotecas estão mapeadas no /etc/ld.so.cache?
- 9. Crie o diretório /home/<seuusuario>/libs/, em seguida copie algumas das bibliotecas existentes no /lib/ para esse diretório, e inclua esse diretório na base do ld.so.
- 10. Quantas bibliotecas externas são utilizadas pelo programa "top"
- 102.4 Gerenciamento de Pacotes Debian
- 11. Faça o download do .deb do shell "ksh"
- 12. Instale o ksh usando o "dpkg"
- 13. Utilizando o apt-get ou o apt, instale o mysql-client
- 14. Utilizando o apt-get ou o apt, remova completamente a aplicação ksh
- 15. Quantos "pacotes" há instalados em seu Linux?
- 16. Quais as dependências da aplicação "bash" ?
- 102.5 Gerenciamento de Pacotes RPM e YUM
- 17. Faça o download do pacote rpm do editor de textos "nano"
- 18. Utilizando o comando rpm, instale o "nano"
- 19. Consulte a versão do nano que foi instalada
- 20. Utilizando o yum, remova o pacote nano
- 21. Utilizando o yum, faça o upgrade de todos os pacotes de sua distribuição RedHat-based, sem remover pacotes obsoletos.
- 22. Encontre a aplicação relacionada ao arquivo /etc/sudoers

### 104.1 Design do Layout do HD

- 1. Adicione em sua máquina virtual um novo disco de 10 GB e crie o seguinte conjunto de partições utilizando o modelo MBR:

* /dev/sdX1 - 3G
* /dev/sdX3 - 2G
* /dev/sdX4 - O restante do disco
* /dev/sdX5 - 500M
* /dev/sdX6 - 1500M
* /dev/sdX7 - 2G

- 2. Redimensione a partição de número 7 para que ela tenha o tamanho de 3G ao invés de 2G.
- 3. Defina a partição sdX5 para que ela seja utilizada na área de swap
- 4. Formate as partições 1 e 3 como ext4, a partição 6 como XFS e a 7 como Btrfs.
