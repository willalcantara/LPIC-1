# Linux

## 103  Comando GNU E Unix
### 103.1 Trabalhando com linha de comando (4 Peso)
#### Tipos de Shell
- Sh - 
- Csh – Implementa recurso da linguagem C
- sh - 
- Bash – evolução do csh

Como saber ?
~~~bash
Echo $SHELL
~~~
Comandos externos e internos
-	Type echo
-	Bultin(comando interno)
-	Command is Hashed(cache interno)
-	Command is /bin/tar (programa interno)
-	*is hashed(/usr/bin/clear) – está em cache
-	Echo $PATH(Exibe os diretórios que estão no caminho), indica os caminhos onde o Type irá pesquisar para encontrar os comandos/programas externos

E se não estiver no $PATH?
-	Preciso localizar o programa
### variaveis
- Local: processos iniciados a partir do shell não enxergam a variável.
-Como exportar
~~~bash
	Export “nome da variável”
~~~

- Posso criar a variável já exportada (export Nome_variavel =valor)
- Set – mostra todas as variáveis
- Env – Mostra apenas as variáveis que são globais, o que foi exportado,
- Pode alterar o valor da variável para uma execução.
- Unset – remove uma variável
- Algumas variáveis interessantes
- HISTFILE = Mostra onde está o arquivo com o histórico de comando
- LOGNAME = Quem fez o login nesta sessão.
- PWD = Diretório em que você está.
- TERM = Qual interface gráfica você está.

Variáveis dinamicamente definidas pelo shell, são definidas pelo shell.

Exemplos

- \$$ Mostra o PID do processo atual (do shell ou script que esteja executando)
- $! Mostra o último processo executado em background.
- $? Mostra o código de retorno do último código que você executou.
- ~ Mostra o home do usuário atual
- ~ + nome do usuário, mostra o home do usuário root
- Mais algumas variáveis de ambiente
- DISPLAY: Indica às aplicações gráficas onde as janelas deverão ser exibidas. Será estudado no Tópico 106.
- HISTFILE: Arquivo do histórico de comandos
- HISTFILESIZE: Quantidade de linhas/comandos armazenados no arquivo de histórico
- HOME: Indica o diretório do usuário atual
- LOGNAME e USER: Nome do usuário atual
- PATH: Diretórios em que o Linux irá procurar por arquivos executáveis
- PS1: Aparência do prompt do shell.
- PWD: Diretório atual
- OLDPWD: Diretório anterior

Executando comandos em sequência: a cada comando, digite o ; (ponto e vírgula)

& (e comercial): executa o segundo comando se o 1º for executado com sucesso.

||(Pipe Pipe): executa o segundo independente do 1º.

- History: exibe os seus últimos comandos
- !!: repete o último comando executado
- !n: n sendo o número do comando, ele repete o comando executado
- ![string]: executa o último comando que contém a string
- Como limpar? History -c
-  Set | grep HISTFILE
- CTRL+ R : pesquisa do comando executado

### Como obter ajuda? Man [comando]
- Dentro do man ,utilize [/string] para pesquisar
- Quando o comando é interno, você precisa pesquisar o manual do bash
- Info[comando] referência rápida do comando
- Man -k “system information”, exemplo, ele traz todos os comandos que contém o “system information”
- Whatis [comando], mostra a informação deste comando
- apropos, igual o man-k
- uname: imprime informações do sistema
- uname -r: versão do kernel
- alias: forma de criar um atalho para o comando
- alias lt=’ls /tmp’
- which :  localiza um comando dentro dos diretórios da variáveis $PATH
- Quotting: Uso de aspas duplas, simples e barra de proteção(\escape).
	Exemplos: 
  ~~~bash
  echo “*”, ele impede a execução do *, então só exibe o *
  ~~~~
- Aspas duplas: protege todos exceto $cifrao /barra invertida e `crase

### 103.2 Aplicando filtros a textos e arquivos de textos

- Cat -n – todas as linhas numeradas
- Cat-b, todas as linhas, exceto as brancas
- Cat -s, transforma as linhas brancas em 1 linha só
- Cat -A, exibe caracteres especiais, tab e enter.
- Tac, imprime o arquivo de tras para frente.
- Head, exibe o cabeçalho do arquivo
- Head -n2, só as duas primeiras linhas
- Head -c100, só os cem primeiros bytes
- Tail -5, exibe as últimas 5 linhas
- Tail -f, exibe as linhas e aguarda a edição dos arquivos
- Less: faz a paginação dos arquivos. “barra de espaço” vai para a próxima pagina
- O “/” procura a palavra, n busca a próxima ocorrência e o N maiúscula volta a pesquisa.
- CTRL + G, status do arquivo
- Wc, lê as quantidadades de palavras,linhas,bytes e caracteres.
- Nl – le o conteúdo, numera as linhas e desconsidera as linhas em branco
- Sort – ordena o arquivo
- Sort -r – ordena de maneira reversa
- Sort -k2, ordena pelo segundo campo
- Uniq: apenas ocorrências únicas e sequenciais
- Uniq –d mostra apenas linhas duplicadas
- Uniq -c mostra as linhas duplicadas e contadas
- Expand – converte de tab para espaços, sem alterar, apenas trata
- Unexpand -a – converte espaços para tab, sem alterar, apenas trata
- Expand -t 5 -a  - altera quantos caracteres viram um tab
- Od- Exibe o conteúdo de um texto em formato octal.
- Od -tx – exibe em hexadecimal
- Join -  combina dois arquivos através de um índice
- Paste – combina linha a linha
- Spilt – l20 – divide um arquivo em vários outros.
- Split -b100 : divide em 100 bytes	
- Tr – pegar um conteúdo e substituir ou deletar. No Tr nós informamos via pipe ou redirecionamento de entrada.
- Exemplo
~~~bash
cat alunos.txt | tr a-z A-Z  && cat alunos.txt | tr [:upper:] [:lower:] && cat alunos.txt | tr " " "_"
~~~
- Exemplo 2
~~~Bash
echo "curso de Linuuux" | tr -s u
~~~

- Fmt – formata uma saída de texto, vamos supor que você queira reduzir o tamanho da linha na tel. Ele tem o padrão de 75 caracteres por linha, você pode modificar com o parâmetro “-w”.
- Pr -l 50 - Prepara o arquivo para a impressão. {o -l 50 define que é 50 linhas por pagina}
- Exemplo:
~~~Bash
pr -l 30 -h "Curso LPI 1"  arquivolongo.txt
~~~

Cut – recorta partes de um texto.
~~~bash
cut -c5-10 alunos.txt

cut -b1-5 alunos.txt
~~~
- Cut -d” “ -f1 alunos.txt. Define o delimitador e exibe somente o campo1.
- Sed – usado para procurar um conteúdo e substituir o conteúdo.
~~~Bash
Sed ‘ s/Silva/Souza’ arquivoaluno.txt #somente uma vez
Sed ‘ s/Silva/Souza/g’ arquivoaluno.txt #funciona de forma recursiva
Sed ‘3,5 d’ arquivoaluno.txt
Sed ‘/Claudia/d’ arquivoaluno.txt
~~~
- Xzcat -  le o arquivo do tipo texto compactado xz
- Bzcat - le o arquivo do tipo texto compactado bz
- Zcat - le o arquivo do tipo texto compactado gz

- Algoritmos de arquivos – analisa o arquivo e cria uma sequencia de caracteres que representa estes arquivos.

    - Md5sum
    - Csha256sum
    - Sha512sum
    - Sha1sum
Exemplos:
~~~Bash
Sha256 arquivo.iso
Sha256sum -c arquivo #compara o arquivo sum com os outros arquivos do diretório e informa qual está igual.
~~~


