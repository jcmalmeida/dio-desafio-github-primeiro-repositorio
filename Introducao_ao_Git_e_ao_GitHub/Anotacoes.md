# Anotações - Introdução ao Git e ao GitHub - DIO
Essas são anotações realizadas durante o curso “Introdução ao Git e ao GitHub” oferecido pela [DIO](https://dio.me/sign-up?ref=ZFBACACJMY) e faz parte de um dos desafios de projeto da plataforma de ensino de programação.

### 1. Introdução ao Git e sua importância
O Git foi criado em 2005 e é **um sistema de versionamento de código distribuído** criado por Linus Torvalds. O Git surgiu da necessidade de versionamento dos códigos do kernel do Linux e da insatisfação do Linus com as opções de sistemas de versionamento existentes naquele momento.
O GitHub é um serviço mantido atualmente pela Microsoft e que implementa o Git, mas existem outros semelhantes (como BitBucket e GitLab), portanto Git e GitHub não devem ser confundidos como sendo a mesma coisa.
Os **beneficios** de se aprender sobre o Git e GitHub:
* Controle de versão
* Armazenamento em nuvem
* Trabalho em equipe
* Melhoramento do código
* Reconhecimento

### 2. Navegação via command line (CLI) e instalação

**GUI (graphical user interface)** -> interface gráfica, é a forma padrão pela qual a maioria dos usuários de computadores interagem com esses dispositivos (clicar, arrastar, selecionar, etc)

**CLI (command line interface)** -> não tem interface gráfica, é a forma padrão pelo qual o Git foi implementado para uso.

**Comandos mais utilizados no Terminal**
**Windows (terminal derivado do Shell):**
* `cd` -> altera diretório de trabalho;
* `dir` -> lista itens (pastas e arquivos) presentes no diretório atual;
* `mkdir` -> cria uma nova pasta;
* `del` -> deleta arquivos contidos numa certa pasta;
* `rmdir` -> deleta pasta e arquivos contidos nela (vide mais abaixo argumentos).
**Unix (terminal derivado do Bash):**
* `cd` -> altera diretório de trabalho;
* `ls` -> lista itens (pastas e arquivos) presentes no diretório atual;
* `mkdir` -> cria uma nova pasta;
* `rm -rf` -> deleta pasta e arquivos contidos nela recursivamente (r = recursivo, f = force).

Alguns exemplos de comandos e variações de argumentos:
* `cd /` -> altera para o diretório raiz;
* `cd ..` -> volta um nível em relação ao diretório atual;
* `cls` -> limpa a tela no Windows;
* `clear` -> limpa a tela no Unix (ou CTRL + L no teclado);
* TAB (teclado) -> tem a função de autocompletar o que está sendo digitado;
* `echo hello` -> retorna `hello` no terminal;
* `echo hello > hello.txt` -> cria um arquivo `hello.txt` no diretório atual, com o texto `hello` dentro;
* `rmdir folder /S /Q` -> deleta o diretório `folder` e todo o seu conteúdo

**Silence on success** -> caso o terminal não retorne, é provável que o comando dado tenha sido executado com sucesso

**Instalação do Git**

A instalação do Git difere a depender do sistema operacional utilizado. Para maiores informações, consultar diretamente o site: https://git-scm.com

### 3. Entendendo como o Git funciona por baixo dos panos

**SHA1** -> a sigla SHA significa Secure Hash Algorithm (Algoritmo de Hash Seguro), é um conjunto de funções hash criptográficas projetadas pela NSA (Agência Nacional de Segurança dos EUA). A encriptação gera um conjunto de caracteres identificador de 40 dígitos único. Exemplo:
* ao rodar o comando `echo “ola mundo” | openssl sha1`, o terminal retorna a hash `d9802fa01c4c1dfc4ddaf61f766d8d56ad8a8699`;
*  ao rodar o comando `echo “ola mundoa” | openssl sha1`, o terminal retorna a hash `0e7cc97ec8739e0555da9cf5697a5b46d05a60e5`. Veja que foi adicionado apenas um caracter à string, mas a hash gerada é completamente diferente.

**Objetos fundamentais do Git**

**Blobs** -> são estruturas objeto que contêm metadados (tipo de objeto - `blob`, tamanho do arquivo, `\0` e o conteúdo do arquivo)

**Trees** -> são árvores que armazenam os **blobs**. Contêm metadados (tipo de objeto - `tree`, `\0`, guarda o nome e localização dos arquivos (**blobs**) ou outras árvores (diretórios que contém outros diretórios, formando uma estrutura recursiva). Quando um único arquivo é alterado em qualquer subnível de uma árvore, seu **SHA1** é alterado e, por consequência, o **SHA1** da árvore também é alterado, permitindo indicar que houve modificação naquela estrutura.

**Commits** -> é o objeto mais importante de todos e encapsula os demais. O **commit** aponta para um árvore, um parente (último **commit** realizado antes dele) e contém metadados: tamanho, autor, mensagem e registro do tempo (timestamp).  O **SHA1** do **commit** é o hash de toda a informação contida dentro dele e qualquer alteração realizada em qualquer nível abaixo dele irá se refletir na alteração desta hash.
Essa estrutura é o que faz o GIT ser um sistema tão seguro para versionamento de repositórios de maneira distribuída.

**Autenticação no GitHub**

Pelo fato de o GitHub estar descontinuando a autenticação de operações Git via usuário e senha, foram apresentadas duas opções de acesso:
* **Chave SSH** -> é a mais prática pois, uma vez configurada, dispensa ficar digitando/inserido informações a cada operação. Checar orientação no site do GitHub: https://docs.github.com/pt/authentication/connecting-to-github-with-ssh
* **Token** -> checar orientação no site do GitHub: https://docs.github.com/pt/authentication/keeping-your-account-and-data-secure/about-authentication-to-github

### 4. Primeiros comandos com Git

Dentro do terminal, na pasta onde se deseja iniciar um projeto versionado pelo Git, deve-se inserir o comando `git init`. Será criada uma pasta oculta `.git` que pode ser visualizada por meio do comando `ls -a`.

Se for a primeira vez utilizando o Git, é necessário configurar o nome (`SeuNome`) e email (`seuemail@email.com`) para que, ao gerar o commit, haja um autor atrelado a ele. É necessário rodar os comandos `git config --global user.mail seuemail@email.com` e `git config —global user.name SeuNome`. Caso se deseje que essa configuração valha apenas para este repositório, deve-se remover a flag `—global` dos comandos.

Para criar o primeiro commit no repositório, é necessário usar os comandos `git add *` e `git commit -m “Commit inicial”`. O commit deve indicar a alteração realizada, por isso a necessidade de uma mensagem, no caso, `“Commit inicial”`.

Nas próximas aulas, é descrito em mais detalhes a lógica por trás dos comandos aqui descritos.

### 5. Ciclo de vida dos arquivos no Git

**Diretório x Repositório** -> ao se usar o comando `git init`, está sendo criado um repositório do GIT dentro do diretório/pasta desejada.

Estados de arquivo rastreado (**tracked**) pelo Git:
* **Unmodified** -> arquivo ainda não foi modificado;
* **Modified** -> arquivo originalmente **unmodified** que sofreu alguma alteração (alteração é detectada por meio do SHA1);
* **Staged** -> o arquivo está aguardando para fazer parte de um **commit**. Depois disso, ele volta para o estado **unmodified**.
Caso o arquivo não esteja sendo rastreado pelo Git, o seu estado é **untracked**.

Repositórios e ambientes:
* **Servidor**
	* **Repositório remoto** -> exemplo: GitHub, BitBucket, etc
* **Ambiente de desenvolvimento**
	* **Diretório de trabalho**
	* **Área de staging** -> armazena arquivos que estavam **untracked** e foram adicionados pelo comando `add` do Git, bem como arquivos modificados (**modified**), também adicionados a **staged** com o comando `add`;
	* **Repositório local** -> é para onde os arquivos vão ao fazer um **commit**. É de onde os arquivos podem ser enviados para o **repositório remoto**.

O comando `git status` permite monitorar os estados dos arquivos rastreados pelo Git.

Para mover arquivos para o estado de **staged**, usa-se:
* `git add nomeArquivo` -> adiciona um arquivo específico cujo nome é `nomeArquivo`;
* `git add *` ou `git add .` -> adiciona todas as modificações realizadas no diretório.
Para realizar um commit, usasse o comando `git commit -m “msg”`, onde `˜msgs"` contém a descrição das modificações realizadas.

### 6. Introdução ao GitHub

Depois de criada uma conta no GitHub, é necessário se certificar de que o autor configurado no Git da máquina local tem os mesmos dados cadastrados no GitHub. Para isso, é possível usar o comando `git config --list` para visualizar estas informações. Para alterar, é preciso reescrevê-las usando os comandos `git config —global unset user.email` e `git config —global unset user.name`, seguido de `git config --global user.mail seuemail@email.com` e `git config —global user.name SeuNome`.

Para começar um novo projeto, deve-se criar um novo repositório no GitHub para este projeto. O próprio serviço mostra instruções de como criá-lo na máquina local e ligá-lo ao GitHub, mas também como subir um projeto já existente na máquina local. Neste segundo caso, assumindo que o projeto já tenha um commit, na pasta que contém os arquivos deve-se usar o comando `git remote add origin https://github.com/SeuNome/projeto.git` para ligá-lo ao GitHub, e `git push -u origin master` para subir os arquivos para a plataforma.
Para mostrar as listas de repositórios remotos cadastrados, deve-se usar o comando `git remote -v`.

### 7. Resolvendo conflitos

Suponhamos que dois usuários (A e B) sejam mantenedores de um certo repositório no GitHub. No momento inicial, ambos tem a mesma versão do repositório em suas máquinas locais, mas após um certo tempo, o usuário A faz uma alteração no código e atualiza o repositório no GitHub. Caso o usuário B faça uma alteração e tente subí-la depois disso, haverá um conflito e o próprio Git irá sugerir a ele atualizar o repositório em sua máquina para a versão mais recente presente no GitHub. Neste caso, o usuário B deve executar o comando `git pull origin master`. Neste momento, o Git irá sinalizar o ponto onde existe conflito entre a versão presente no GitHub e a versão presente na máquina do usuário. Ele deverá resolver isso manualmente, gerar um novo commit e então subir os arquivos para o GitHub.

Caso uma pessoa deseje ter acesso a um repositório online para, por exemplo, contribuir com ele, ela deve baixá-lo para sua máquina com o comando `git clone urlDoProjeto`. No comando, a `urlDoProjeto` é o código informado diretamente pelo GitHub (HTTPS ou SSH). O diretório baixado é verdadeiramente um repositório pois já tem a pasta Git e aponta corretamente para o repositório online (pode ser checado com o comando `git remote -v`).

### 8. Extras

Link para a DIO:

[https://www.dio.me/](https://dio.me/sign-up?ref=ZFBACACJMY)

Artigo explicando como editar arquivos de texto diretamente no terminal do Linux ou MacOS:

[https://medium.com/@charlesopokuagyemang/reading-and-editing-files-with-linux-and-mac-os-terminal-commands-3a797a27ed1b](https://medium.com/@charlesopokuagyemang/reading-and-editing-files-with-linux-and-mac-os-terminal-commands-3a797a27ed1b)

Sintaxe básica de Markdown:

[https://www.markdownguide.org/basic-syntax/](https://www.markdownguide.org/basic-syntax/)