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

	Export “nome da variável”
-   
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
