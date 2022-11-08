
## :triangular_flag_on_post: Forensics 101

**Descrição**: Think the flag is somewhere in there. Would you help me find it? <https://mega.nz/#!OHohCbTa!wbg60PARf4u6E6juuvK9-aDRe_bgEL937VO01EImM7c>

### O que eu fiz

1. Baixei o arquivo e analisei o Metadata pela ferramenta **exif.tools**, mas não encontrei nada lá.
2. Então resolvi converter a imagem em string **<https://www.fileformat.info/tool/strings.htm>** </br>
E encontrei a flag

## :triangular_flag_on_post: WOW... So meta

**Descrição**: This photo was taken by our target. See what you can find out about him from it. <https://mega.nz/#!ifA2QAwQ!WF-S-MtWHugj8lx1QanGG7V91R-S1ng7dDRSV25iFbk>

</br>

Esse eu fui direto na ferramenta **exif.tools** e encontrei a flag.

## :triangular_flag_on_post: Git Is Good

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

## :triangular_flag_on_post: Exif

**Descrição**:

If only the password were in the image?

<https://mega.nz/#!SDpF0aYC!fkkhBJuBBtBKGsLTDiF2NuLihP2WRd97Iynd3PhWqRw> You could really ‘own’ it with exif.

### O que eu fiz

Esse eu fui direto na ferramenta **exif.tools** e encontrei a flag. </br>
Outra ferramenta que eu poderia ter usado: **aperisolve**

## Binwalk

**Descrição**: Here is a file with another file hidden inside it. Can you extract it? <https://mega.nz/#!qbpUTYiK!-deNdQJxsQS8bTSMxeUOtpEclCI-zpK7tbJiKV0tXYY>
</br>

```md
Um arquivo dentro de um arquivo.
```

### O que eu fiz

O arquivo era uma imagem e possívelmente uma imagem dentro de uma imagem. </br>
Eu usei a ferramenta [binwalk](https://github.com/ReFirmLabs/binwalk) para extrair e encontrei esse [tutorial](https://www.linkedin.com/pulse/forense-analisando-arquivos-com-binwalk-bruno-izid%C3%B3rio/?originalSubdomain=pt)

```bash
git clone https://github.com/ReFirmLabs/binwalk.git
cd binwalk
sudo python3 setup.py install
```

1. Descobrir o arquivo que está dentro da imagem:

```bash
binwalk caminho/nomeDoArquivo.extensao
# binwalk PurpleThing.jpeg
```

Retornou um PNG

```bash
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 780 x 720, 8-bit/color RGBA, non-interlaced
41            0x29            Zlib compressed data, best compression
153493        0x25795         PNG image, 802 x 118, 8-bit/color RGBA, non-interlaced
```

2. Agora extrair:

Extraindo manualmente: </br>

```bash
-D ou -dd=<Tipo:Extensão:Comando>
```

O formato usado para extrair a regra especificada é:

**Tipo:Extensão:Comando** </br>

- **Tipo**: string, em “caixa baixa”, para informar o tipo do arquivo que se quer extrair;

- **Extensão**: define qual será a extensão que o arquivo será salvo no diretório. Por padrão, o binwalk não coloca nenhuma extensão;

- **Comando**: é um argumento opcional para ser executado após a extração para o diretório.

```bash
binwalk --extract --dd=".*" caminho/nomeDoArquivo.extensao
```

3. Agora é abrir o diretório extraído **_PurpleThing.jpeg.extracted** :

```bash
ls 
API.md    README.md   images
Dockerfile   _PurpleThing.jpeg.extracted setup.py
INSTALL.md   build    src
LICENSE    deps.sh    testing
NOTICE.md   dist
```

4. E lá estava o arquivo com a flag.
