# Exercicios

Os exercícios a seguir tem a finalidade principal de revisar e praticar o que estudamos durante as aulas, no entanto, você também pode ser desafiado a descobrir novas opções ou formas de uso dos comandos, inclusive combinando comandos estudados em diferentes sub-tópicos.

## 103.1 Trabalhando na Linha de Comando

1. Encontre as seguintes informações sobre a sua instalação Linux:
   - O caminho completo do arquivo .bash_history para o seu usuário;
   - O release do kernel instalado
   - Os diretórios incluídos em seu PATH
   - O hostname da máquina
   - O PID da sua sessão shell atual
2. Crie e exporte uma variável chamada "NOME" que contenha o seu nome completo.
3. Crie um comando que escreva na tela a seguinte frase: "O Nome do Próximo Certificado LPI 1 é: <utilize a variável NOME>"

## 103.2 Aplicando Filtros a Textos e Arquivos

4. O arquivo /etc/passwd contém a lista de usuários do Linux, os campos são separados pelo caractere :, o primeiro campo indica o nome do usuário e o terceiro o ID do usuário.
   Escreva um comando que mostre os últimos 15 registros do arquivo, exibindo apenas o nome do usuário e seu ID, e que esteja ordenado pelo ID numérico. Por exemplo:

- usuario1:10
- usuario2:12
- usuario:3:1000
  .......

5. Gere um comando, ou sequência deles, que mostre o número de linhas do arquivo /etc/passwd excluindo-se as linhas que contenham a palavra "daemon". O resultado do comando deve ser o número de linhas.

## 103.3 Gerenciamento Básico de Arquivos

6. No home de seu usuário, crie um diretório chamado LPI1, dentro dele crie Aulas, Exercicios e Exemplos.
7. Copie (não mova) todos os arquivos e diretórios existentes em /etc/network/ para <HOME>/LPI1/Exercicios/Network/. Mantenha as mesmas permissões.
8. Copie (não mova) todos os arquivos do diretório /etc, cujo norme termine com ".conf" para <HOME>/LPI1/Exercicios/Config/
9. Em <HOME>/LPI1/Exercicios, crie um arquivo chamado arquivos-cron.tgz, compactado com o gzip, contendo todos os arquivos e diretórios do /etc que contenham a palavra "cron" no nome.
10. Descompacte conteúdo do arquivo arquivos-cron.tgz dentro do diretório <HOME>/LPI1/Exercicios/Descompactar/
11. Encontre todos os arquivos do diretório /var, cujo nome termine com ".gz" e que foram modificados nas últimas 48 horas.

## 103.4 Fluxos, Pipes e Redirecionamentos

12. Gere um comando que crie um arquivo chamado diretorios-config.out, contendo a saída do "ls -l" para todos os diretórios do /var cujo nome contenha a palavra "config". A saída deve ser algo como o visto abaixo:
    drwxr-xr-x 2 root root 4096 Mar 28 11:49 /var/cache/fontconfig
    drwx------ 2 root root 4096 Abr 7 11:37 /var/cache/ldconfig
    drwxr-xr-x 2 lightdm lightdm 4096 Mar 27 16:41 /var/lib/lightdm/.cache/fontconfig
    drwx------ 4 lightdm lightdm 4096 Mar 27 16:41 /var/lib/lightdm/.config

13. Explique as diferenças entre os seguintes redirecionadores de entradas e saídas

- • > arquivo :
- • < arquivo :
- • >> arquivo :
- • 2> arquivo :
- • >arquivo 2>&1 :

14. Escreva um único comando comando que gere a lista de arquivos e diretórios contidos em ~/LPI1/Exercicios/Network, exibindo-os na tela e em um novo arquivo chamado lista-network.out

## 103.5 Criar, Monitorar e Encerrar Processos

15. Preencha as informações abaixo com os dados de sua instância Linux:

- • Total de Memória RAM utilizada (em MB):
- • Load Average (Média dos Últimos 5 minutos):
- • Quantidade de Processos em Execução:
- • PID dos 3 processos que estão utilizando mais Memória:
- • PPID (Parent Process ID) dos 3 processos com maior tempo de Uso de CPU:

16. Crie um comando, que gere um arquivo chamado ~/LPI1/Exercicios/resultado-top.out, que contenha a saída do comando top, atualizado a cada 10 segundos, sendo executado indefinidamente até que o processo seja morto. O comando deve rodar em background.
17. Envie um sinal de SIGKILL para o processo iniciado no exercício 16.

## 103.6 Modificar a Prioridade de Execução de Processos

18. Inicie o mesmo comando aplicado no exercício 16, porém com a menor prioridade possível.
19. Altere o NICE do processo "rsyslogd" para o valor -10.

## 103.7 Pesquisar arquivos de texto com Expressões Regulares

20. Gere um comando que exiba na tela todas as linhas do arquivo /etc/passwd que terminem com "nologin"
21. Crie um comando que liste todos os arquivos do diretório /etc/ que contenham a palavra "eth0" em seu conteúdo, não no nome do arquivo. A pesquisa deve incluir também os subdiretórios. Apenas o nome e caminho do arquivo deve ser exibido.
22. No arquivo /etc/passwd, o primeiro campo indica o nome do usuário, enquanto que o terceiro indica o ID do usuário. Crie um comando que exiba apenas os nomes de usuários que tenham o ID com 3 dígitos.

## 103.8 Edição básica de Arquivos Usando o VI

23. Crie um arquivo texto chamado meu-curriculo.txt. Nele inclua as seguintes seções:

- • Dados Pessoais: Contendo nome, idade, endereço e telefone
- • Experiência Profissional: Nome das 3 últimas empresas em que trabalhou
- • Cursos Realizados: Nome dos últimos 3 cursos que realizou, pode incluir este.
- • Certificações Obtidas: Todas as suas certificações. Já pode incluir a LPIC-1 como uma delas ;)
- • Seu Objetivo de Carreira para os Próximos 5 anos.
- • Salve e saia do arquivo.

24. Abra novamente o arquivo meu-curriculo.txt, faça as seguintes modificações:

- • Mova a seção de "Objetivo" para que ela fique após os "Dados Pessoais"
- • Após o ítem "Experiência Profissional", adicione a seção "Formação Escolar", incluindo informações de escolaridade (ensino médio, técnico, superior, pós e etc)
- •Salve e saia do arquivo.
