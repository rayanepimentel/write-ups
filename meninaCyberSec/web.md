# Capture The Flag - Menina de CyberSec

# CTF

CTF (Capture The Flag) realizado entre os dias 12 e 15 de Novembro, no servidor Menina de CyberSec.

# WEB

## Desafio: Não odeio o JavaScript! :triangular_flag_on_post

<code>formato da flag **MCS{xxxx_xxxx_xxxx_xxx}**</code>

```
Esse desafio tinha um arquivo .txt e ao abri-lo, tinha endereço do site para analisarmos.
```

### Análise

No site tinha 2 buttons e um me chamou atenção, ao clicar aparecia a seguinte mensagem:

```bash
Secrets can only be accessed by admin
```

A palavra **admin** poderia me levar para algum diretório. </br>
Tentei passar na URL<strong>/admin</strong> e retornou:

```bash
403 Forbidden
```

Status code 403 de não permitido. Diretório existe, mas eu não tenho permissão. </br>

Utilizando a ferramenta <strong>dirbuster</strong>, me retornou algumas portas <strong>200</strong>, ou seja portas que não precisam de autorização para acessar.</br>
E uma delas me chamou a atenção:
```bash
200 /admin/admin.js
```
E nesse arquivo estava a flag

> "MCS{3num3r4t10n_F0rfun_4nd_Pr0f1t}"
