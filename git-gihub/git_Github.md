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

Tutorial on-line --> https://www.freecodecamp.org/portuguese/news/como-gerenciar-diversas-contas-do-github-em-uma-unica-maquina-com-chaves-ssh/

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


## Sincronizando um fork com o repositorio original

Você está contribuindo com um projeto de codigo fonte aberto e percebeu que o seu fork esta fora de sincronia com o repositorio original.

voce fez o fork do projeto original
e clonou na sua máquina

como arrumar:

1. Durante o processo de clonagem o git nomeou meu repositório remoto de “origin”:
ex.

$ git remote --verbose
origin git@github.com:plainspooky/bootstrap.git (fetch)
origin git@github.com:plainspooky/bootstrap.git (push

Ele será utilizado por padrão durante a execução dos comandos git fetch e também do git push. Mas é possível acrescentar outros repositórios remotos como, por exemplo, o repositório original do Bootstrap!

Adicionar um novo remote para o projeto original

$ git remote add upstream https://github.com/twbs/bootstrap.git

Foi usado o nome de "upstream" mas pode-se utilizar qualquer outro nome

faça o teste, digite:

$ git remote --verbose

Resutado:

origin	git@github.com:plainspooky/bootstrap.git (fetch)
origin	git@github.com:plainspooky/bootstrap.git (push)
upstream	https://github.com/twbs/bootstrap.git (fetch)
upstream	https://github.com/twbs/bootstrap.git (push)

3. Atualizando ambos os repositórios

para sincornizar o repositorio local, primeiro atualize o upstream

$ git checkout master

$ git fetch upstream

remote: Counting objects: 54, done.
remote: Total 54 (delta 40), reused 40 (delta 40), pack-reused 14
Unpacking objects: 100% (54/54), done.
From https://github.com/twbs/bootstrap
   a3e45d8ce..7b9c8e8eb  v4-dev     -> upstream/v4-dev

$ git rebase upstream/master
Current branch master is up to date.

O git fetch apenas baixará os commits (objetos) do repositório mas não mexerá no conteúdo local, o git rebase se encarregará da tarefa de reorganizar os commits para deixar seu repositório tal qual o “upstream”. O único cuidado aqui é usar o git rebase sempre dentro do mesmo ramo que se deseja sincronizar.

Como como não havia diferenças entre os ramos “master” em “origin” e “upstream” nada foi alterado. Mas aproveitando que o fetch trouxe um novo ramo, vamos atualizá-lo também, primeiro indo para ele.

$ git checkout v4-dev

Switched to branch 'v4-dev'
Your branch is up to date with 'origin/v4-dev'.

Depois atualizando a lista de commits.

$ git rebase upstream/v4-dev

First, rewinding head to replay your work on top of it...
Fast-forwarded v4-dev to upstream/v4-dev.

Daí subir as mudanças para o repositório remoto.

$ git push 

Counting objects: 60, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (57/57), done.
Writing objects: 100% (60/60), 6.78 KiB | 6.78 MiB/s, done.
Total 60 (delta 42), reused 5 (delta 2)
remote: Resolving deltas: 100% (42/42), completed with 23 local
objects.
To github.com:plainspooky/bootstrap.git
a3e45d8ce..7b9c8e8eb v4-dev -> v4-dev

E pronto, repositórios atualizados.

commit 7b9c8e8eb34618f294ee6585aaa866205402bb49 (HEAD -> v4-dev,
upstream/v4-dev, origin/v4-dev, origin/HEAD)
Author: Herst <Herst@users.noreply.github.com>
Date: Mon Sep 3 17:55:04 2018 +0200

Detalhe para o fato de que o ID do commit que referencia o ramo “v4-dev” é o mesmo tanto em “origin” quanto em “upstream”, ou seja, o histórico dos commits dos repositórios estão iguais novamente.



