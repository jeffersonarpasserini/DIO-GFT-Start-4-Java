# GIT/Github

## Configurações Iniciais

- git config --global init.defaultBranch main
- git config --global user.email "email@email.com"
- git config --global user.name usuario_github
- git config --list

## Zerar alguma configuração
- git global unset "propriedade"

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

## Outra forma: token de acesso pessoal



#### Associa repositorio local ao remoto
- git remote add origin "endereço ssh fornecido pelo github"

#### verifica o status
- git remote -v

#### envia arquivos para o servidor
- git push origin main

#### atualiza o repositorio local a partir do remoto
-git pull origin main

#### clona um repositorio remoto
- git clone "link ssh do github"



