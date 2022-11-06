# Capture The Flag - Nubank

## CTF de Web

CTF (Capture The Flag) realizado no dia 05/11/2022, no servido Hack Her_Way.

# 1º CTF

## Foothold

Para começar, acessamos o link (já expirado) para encontrar a página inicial do CTF, onde encontramos os desafios.

## Desafio WEB

Eu não tenho a descrição do desafio, mas basicamente era para recuperar o código fonte da aplicação.</br>

Ao tentar acessar a pasta /.git/ era retornado erro de permissão

```bash
Forbidden
```

Como precisava de acesso, procurei vulnerabilidades da pasta .git. Encontrei isso aqui: <https://andrebian.com/oculte-a-pasta-git-de-sua-aplicacao/> </br>

Depois procurei ferramentas que podesse me ajudar a ter acesso a pasta /.git/ </br>
Encontrei: <a href="https://github.com/internetwache/GitTools">GitTools</a> </br> </br>

### Comandos utilizados

Depois de fazer o clone do GitTools, dentro da pasta Drumper:

```bash
./gitdumper.sh http://caminho/.git/ hackDumper
git status    
git checkout -- .  
git log    
```

Entrei na pasta cd hackDumper e depois ls -a e estava a pasta .git/ </br>
Dei um <code>git reset --hard</code> para desfazer as alterações que o hack tinha feito </br>
Eu já tinha o código fonte, mas precisava encontrar a flag. Então voltei na alteração do commit pelo hash, para verificar se tinha algum arquivo que podesse ajudar.<br>

```bash
git checkout hashDoCommit
```

Depois verifiquei o que tinha na pasta <code>ls -a</code> e tinha um arquivo secrets.txt e lá estava a flag.
