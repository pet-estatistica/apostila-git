# Projetos remotos
PET Estatística  
29/10/2015  

## 1. Configuração de conexão ssh com servidor

O git possibilita ao usuário realizar uma chave ssh que fará uma conexão segura da sua máquina com o servidor.

Para obter uma conexão entre a máquina e o servidor, o usuário deve obter uma chave ssh. Para isso começamos com o seguinte comando no terminal:


```sh
## Gerando uma chave ssh
ssh-keygen -t rsa -C "usuario@email.com"

```

A partir deste comando, o usuário poderá alterar o diretório onde será salva a chave ssh. O usuário pode permanecer com o diretório padrão, basta apertar Enter.
Agora foram criados dois arquivos no diretório, **id_rsa** e **id_rsa.pub** 
Depois de escolher o diretório onde serão salvos os arquivos, o usuário terá a opção de digitar uma senha ou deixar o espaço em branco.

Para visualizar a chave basta o usuário digitar o seguinte comando:


```sh
 cat ~/.ssh/id_rsa.pub
```

No arquivo **id_rsa.pub** está a chave. O usuário deve copiar o texto deste arquivo na íntegra.
Para gerar a conexão ssh com o servidor o usuário deve abrir o site [https://gitlab.c3sl.ufpr.br/profile/keys](https://gitlab.c3sl.ufpr.br/profile/keys) e clicar em [Add SSH Key](https://gitlab.c3sl.ufpr.br/profile/keys/new). O usuário deve escrever um título para a sua nova chave, no campo **key** colar o texto copiado do arquivo **id_rsa.pub** e adicionar sua nova chave.

Para checar a configuração da sua máquina com o sevidor basta realizar o seguinte comando:

```sh
ssh -T git@gitlab.c3sl.ufpr.br
```


## 2. Criando um repositório Git

Criar um repositório no Git e clonar na sua máquina:
No link [New project](https://gitlab.c3sl.ufpr.br/projects/new) do gitlab  o usuário deve nomear seu novo projeto (como exemplo nomeamos de **Teste**), escrever uma breve descrição e selecionar a visibilidade dele (private, internal ou public).
Após criar o projeto, uma nova página apresentará instruções com linhas de comando para criar um novo repositório.



```sh
git clone git@gitlab.c3sl.ufpr.br:usuario/Teste.git
cd Teste
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

Acima foi clonado o repositório git na máquina e criado um arquivo **README.md**, esse arquivo aparece na capa do seu no repositório.

Agora o usuário já pode criar e alterar arquivos e transferir estes para seu repositório remoto. Basta utilizar os comandos **git add**, **git commit** e **git push**.


## 3. Os comandos clone, push, pull e fetch

### Git Push

Como apresentado no capítulo anterior (Projetos locais) os comandos **git add** e **git commit** adicionam os arquivos no repositório. A próxima etapa é enviar o arquivo para o repositório remoto. 
Para enviar é necessário o comando **push**:

```sh
git push origin master
```

### Git Pull

Assim como o ** git push **, o ** git pull ** também faz transferência de arquivos, porém são transferidos do repositório remoto para a máquina, este comando faz o merge automaticamente.


```sh
git pull origin master
```

### Git fetch

O ** git fetch ** baixa arquivos do diretório remoto, porém as modificações devem ser atualizadas por um merge.


```sh
git fetch origin master
```

Para verificar as modificações realizadas entre versões de um arquivo basta utilizar o comando ** git diff **:


```sh
git diff master origin/master
```
 
 
### Git clone

O comando **git clone**, mostrado na seção anterior, tem a finalidade de clonar repositórios existentes na máquina do usuário.


```sh
git clone git@gitlab.c3sl.ufpr.br:usuario/Teste.git

```


## 4. Projetos remotos ##

### 4.1 - Configuração de conexão ssh com servidor ###
* Chaves públicas: introdução e breve descrição, facilidade da criação de um repositório devido a disponibilidade do servidor c3sl;
* Criando chave pública ssh: como gerar uma chave pública ssh que realizará uma conexão segura entre a máquina e o servidor;

### 4.2 - Clone, push, pull, fetch ###
* Introdução: colaborando em trabalhos coletivos;
* Clone: como copiar uma um repositório já existente para a sua máquina;
* Push: como transferir committs de um repositório local para um repositório remoto;
* Pull: como importar e mesclar arquivos do repositório remoto para a máquina;
* Fetch: como importar arquivos do repositório remoto para o repositório local, é possível verificar o arquivo antes de integrá-lo ao projeto com o git merge;
* Pull request: como facilitar a colaboração dos desenvolvedores.