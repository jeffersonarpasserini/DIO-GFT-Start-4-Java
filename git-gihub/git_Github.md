# GIT/Github

## Configurações Iniciais

- git config --global init.defaultBranch main
- git config --global user.email "email@email.com"
- git config --global user.name usuario_github
- git config --list

## criando configurações locais

- git config --local user.name JeffersonPasserini
- git config --local user.email "jefferson.passerini@hotmail.com"

# lista configurações locais
- git config --local --list  

## Zerar alguma configuração
- git global --unset "propriedade"

## Ciclo de Vida
- untracked
- unmodified
- staged
- modified

## altera o nome da branch
- git branch -m main

## Comandos
- git init
- git add
- git commit
- git status

## Repositorio remoto

### Gerar Chave (key) para a máquina

- ssh-keygen -t ed25519 -C email_github -> gera chaves publica e privada (colocar a chave publica no github)

- eval $(ssh-agent -s) - coloca o serviço em execução

- ssh-add id_ed25519 (chave privada)

### gerar chave para segundo usuario github

- ssh-keygen -t rsa -C "jefferson.passerini@hotmail.com" -f "id_rsa_hotmail"

crie o acesso ssh no github settings com a nova chave

adicione ao ssh-agent as duas chaves das duas contas
ssh-add id_...
ssh_add id_conta2...

- ssh-add -l  lista todos as chaves vinculadas ao agente
- ssh-add -D remove todas as chaves vinculadas

criar arquivo de configuração para  gerenciar as chaves geradas

### crie o arquivo no diretorio .ssh
touch config
edite o arquivo
code config (pico)

### Coloque o seguinte codigo

# Conta pessoal, a configuração padrão
Host github.com

    HostName github.com

    User git

    IdentityFile ~/.ssh/id_rsa
   
# Conta de trabalho-1

Host github.com-work_user1

    HostName github.com

    User git

    IdentityFile ~/.ssh/id_rsa_work_user1


## Outra forma: token de acesso pessoal


#### Associa repositorio local ao remoto
- git remote add origin "endereço ssh fornecido pelo github"

### Quando existem mais de um usuario
- git clone git@github.com-JeffersonPasserini:JeffersonPasserini/DIO-GFT-Start-4-Java.git

O que estiver entre o @ e o ":" é o conteudo da tag Host do arquivo config

#### verifica o status
- git remote -v

#### envia arquivos para o servidor
- git push origin main

#### atualiza o repositorio local a partir do remoto
-git pull origin main

#### clona um repositorio remoto
- git clone "link ssh do github"





