# 4. Projetos remotos
PET Estatística  
29/10/2015  
    
## 4.1. Criando um repositório Git
    
Primeiramente é necessário ter acesso a um servidor linux com servidor SSH, no qual o usuário poderá ter seus repositórios. Será utilizado um diretório no qual será armazenado o repositório, que será definido como remoto.
No exemplo a seguir é preciso criar um repositório remoto chamado `TesteRep` e o armazenar em um diretório criado `~/git`:
    
**Exemplo:**
    
    ```sh
    # Para criar um diretório git na sua home:
    mkdir ~/git
    # Para criar um repositório git:
    mkdir TesteRep.git
    # Para definir TesteRep como um repositório remoto:
    git --bare init
    ```

As configurações do servidor estão completas. A partir de agora serão dados os primeiros comandos para iniciar o repositório criado.




## 4.2. Configuração de conexão ssh com servidor

O git possibilita ao usuário realizar uma chave ssh que fará uma conexão segura da sua máquina com o servidor.

Para obter uma conexão entre a máquina e o servidor, deverá obter uma chave ssh. Para isso começamos com o seguinte comando no terminal:
    
**Exemplo:**
    
    ```sh
    ## Gerando uma chave ssh
    ssh-keygen -t rsa -C "usuario@email.com"
    ```

A partir deste comando, será possível alterar o diretório onde será salva a chave ssh. O usuário pode permanecer com o diretório padrão, basta apertar Enter.
Agora foram criados dois arquivos no diretório, `id_rsa` e `id_rsa.pub`. 
Depois de escolher o diretório onde serão salvos os arquivos, terá a opção de digitar uma senha ou deixar o espaço em branco.

Para visualizar a chave basta digitar o seguinte comando:
    
**Exemplo:**
    
    ```sh
    cat ~/.ssh/id_rsa.pub
    ```

No arquivo `id_rsa.pub` está a chave. O usuário deve copiar o texto deste arquivo na íntegra.
Para gerar a conexão ssh com o servidor, deve abrir o site [https://gitlab.c3sl.ufpr.br/profile/keys](https://gitlab.c3sl.ufpr.br/profile/keys) e clicar em [Add SSH Key](https://gitlab.c3sl.ufpr.br/profile/keys/new). É necessário escrever um título para a sua nova chave, no campo `key` colar o texto copiado do arquivo `id_rsa.pub` e adicionar sua nova chave.

Para checar a configuração da sua máquina com o sevidor basta realizar o seguinte comando:
    
**Exemplo:**
    
    ```sh
    ssh -T git@gitlab.c3sl.ufpr.br
    ```




## 4.3. Os comandos clone, push, pull e fetch

### Git clone
Este comando é usado para clonar um repositório do servidor remoto para um servidor local. Caso o usuário queira copiar um repositório que já existe para realizar colaborações em um projeto que queira participar. 
O usuário terá acesso a todos os arquivos e poderá verificar as diferentes versões destes.
No exemplo abaixo temos uma bibliotaca Git, chamada "TesteClone", que será clonado da seguinte forma:
    
**Exemplo:**
    
    ```sh
    git clone git@gitlab.c3sl.ufpr.br:pet-estatistica/TesteClone.git
    ```


Desta forma terá um diretório `TesteClone` em seu computador, onde estarão todos os arquivos do projeto nele.

O usuário também terá a opção de clonar o repositório `TesteClone` em um diretório diferente do padrão Git, que no próximo exemplo denominaremos de `DirTeste`:
    
**Exemplo:**
    
    ```sh
    git clone git@gitlab.c3sl.ufpr.br:pet-estatistica/TesteClone.git DirTeste
    ```


### Git Push

Usado para transferência de arquivos entre repositório local e o servidor remoto. Como o nome já diz o comando empurra os arquivos para o servidor remoto.
No exemplo abaixo enviaremos a ramificação, `Branch Master`, para o servidor chamado `origin`:
    
**Exemplo:**
    
    ```sh
    git push origin master
    ```

É importante ressaltar que se dois usuários clonarem ao mesmo tempo, realizarem modificações e enviar os arquivos atualizados ao repositório utilizando o `Git push`, as modificações do usuário (que realizou o push por último) serão desconsideradas. 

### Git Pull

Também utilizado para transferência de arquivos, o comando puxa os arquivos do servidor remoto para o repositório local e faz o merge do mesmo, fundindo a última versão com a versão atualizada.

**Exemplo:**
    
    ```sh
    git pull origin master
    ```

### Git fetch

Assim como o comando `Git pull`, o `Git fetch` transfere arquivos do repositório remoto para o local, porém ele não realiza automaticamente o merge dos arquivos transferidos, o usuário deve fazer o merge manualmente.

**Exemplo:**
    
    ```sh
    git fetch origin master
    ```

Para verificar as modificações realizadas entre versões de um arquivo basta utilizar o comando `git diff`:
    
**Exemplo:**
    
    ```sh
    git diff master origin/master
    ```


