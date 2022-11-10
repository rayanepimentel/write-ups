
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

## :triangular_flag_on_post: Binwalk

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

## :triangular_flag_on_post: Taking LS

**Descrição**: Just take the Ls. Check out this zip file and I be the flag will remain hidden. <https://mega.nz/#!mCgBjZgB!_FtmAm8s_mpsHr7KWv8GYUzhbThNn0I8cHMBi4fJQp8>
</br>

### O que eu fiz

- Fiz o download do arquivo e tentei abrir o arquivo PDF, mas precisava de uma senha.
- Entrei na pasta <code>ls -a</code> e vi um diretório <code>.ThePassword</code>. Pelo nome eu achei que poderia ter algo lá, entrei e vi o arquivo .txt

```bash
#pasta 
ls -a
# veio arquivos e diretórios
cd .ThePassword
ls -a
cat ThePassword.txt
```

- Foi retornado uma senha, usei para abrir o arquivo PDF que estava protegido.
- E a flag estava nesse arquivo.

## :triangular_flag_on_post: Tux

**Descrição**: The flag is hidden inside the Penguin! Solve this challenge before solving my 100 point Scope challenge which uses similar techniques as this one. </br>

### O que eu fiz

- Primeiro eu analisei o metadados da imagem. Usei a ferramenta <code>exif.tools</code> e encontrei um  **Comment**, com um hash. Peguei esse hash e decodifiquei na base64. Retornou uma senha <code> Password: Linux12345</code>
- Com isso eu pensei em usar o <code>binwalk</code>, para ver se tinha um **arquivo dentro de outro arquivo**.

```bash
binwalk caminho/nomeDoArquivo.extensao
# binwalk PurpleThing.jpeg
```

Retornou:

```bash

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
5488          0x1570          Zip archive data, encrypted at least v1.0 to extract, compressed size: 39, uncompressed size: 27, name: flag
5679          0x162F          End of Zip archive, footer length: 22
```

Vi que tinha um arquivo zip e extrai.

```bash
binwalk -e /caminho/arquivo.jpg
```

- Depois entrei na pasta criada e vi que tinha um arquivo .zip

- Cliquei nele para abrir e me pediu a senha, coloquei a senha que eu tinha decodificado lá no inicio.

- E lá estava a flag.

## :triangular_flag_on_post: Pho Is Tasty

**Descrição**: The flag is hidden in the jpeg file. Good Luck! Have some Pho! Solve this challenge before solving my Scope challenge for 100 points.

### O que eu fiz

1. Anlisei o metadados pela ferramenta <code>exif.tools</code> e string pela ferramenta <https://www.fileformat.info/tool/strings.html> mas não encontrei nada suspeito.
2. Depois analisei pela ferramenta <code>binwalk</code>, mas sem sucesso.
3. Resolvi utilizar a ferramentas <code>hexed</code> <https://hexed.it/> </br>
E encontrei a flag, só foi preciso remover os . (pontos)

 Gandalf TheWise
30 pontos Fácil

