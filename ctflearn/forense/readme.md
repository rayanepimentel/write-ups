
## Forensics 101

**Descrição**: Think the flag is somewhere in there. Would you help me find it? <https://mega.nz/#!OHohCbTa!wbg60PARf4u6E6juuvK9-aDRe_bgEL937VO01EImM7c>

### O que eu fiz

1. Baixei o arquivo e analisei o Metadata pela ferramenta **exif.tools**, mas não encontrei nada lá.
2. Então resolvi converter a imagem em string **<https://www.fileformat.info/tool/strings.htm>** </br>
E encontrei a flag

## WOW... So meta

**Descrição**: This photo was taken by our target. See what you can find out about him from it. <https://mega.nz/#!ifA2QAwQ!WF-S-MtWHugj8lx1QanGG7V91R-S1ng7dDRSV25iFbk>

</br>

Esse eu fui direto na ferramenta **exif.tools** e encontrei a flag.

## Git Is Good

**Descrição**: he flag used to be there. But then I redacted it. Good Luck. <https://mega.nz/#!3CwDFZpJ!Jjr55hfJQJ5-jspnyrnVtqBkMHGJrd6Nn_QqM7iXEuc>

</br>

### O que eu fiz

1. Verifiquei os arquivos da pasta com o <code>ls -a</code>, lista os arquivos ocultos.
2. Tinha o arquivo .git e flag.txt, no arquivo flag.txt tinha a flag, mas como texto "protegido".
3. Dei um git log e vi que tinha 3 commits.
4. Precisava voltar no commit anterior para saber o que deve de mudança:

```bash
$ git checkout hasDoCommit
# depois verifiquei o status
$ git status
HEAD detached at 195dd65
nothing to commit, working tree clean
```

5. Como teve uma mudança, já olhei o arquivo flag.txt

```bash
cat flag.txt
```

E a flag estava lá.

## Exif

**Descrição**:

If only the password were in the image?

<https://mega.nz/#!SDpF0aYC!fkkhBJuBBtBKGsLTDiF2NuLihP2WRd97Iynd3PhWqRw> You could really ‘own’ it with exif.

### O que eu fiz

Esse eu fui direto na ferramenta **exif.tools** e encontrei a flag. </br>
Outra ferramenta que eu poderia ter usado: **aperisolve**
