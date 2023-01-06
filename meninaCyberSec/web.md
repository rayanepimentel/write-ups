# Capture The Flag - Menina de CyberSec

# CTF

CTF (Capture The Flag) realizado entre os dias 12 e 15 de Novembro, no servidor Menina de CyberSec.

# Ferramentas

- Sistema operacional kali
- gobuster

# Desafio WEB

![](/meninaCyberSec/pics/web2.png)

## Desafio: Não odeio o JavaScript! :triangular_flag_on_post:

<code>formato da flag **MCS{xxxx_xxxx_xxxx_xxx}**</code>

```
Esse desafio tinha um arquivo .txt e ao abri-lo, tinha endereço do site para analisarmos.
```

### Análise

1. Analisei o page source
2. Na pagina tinha dois buttons, cliquei em ambos com o console e network abertos.

O segundo button me chamou atenção. Ao clicar exibia a seguinte mensagem na página:

```bash
Secrets can only be accessed by admin
```

A palavra **admin** poderia me levar para algum diretório ou poderia existir um diretório de login</br>
Tentei acessa a URL com o <strong>/admin</strong> e retornou:

```bash
403 Forbidden
```

Status code **403** de não permitido. Diretório existe, mas eu não tenho permissão. </br>

Utilizando a ferramenta <strong>gobuster</strong> técnica de bruteforce para encontrar objetos, arquivos e diretórios do site, me retornou algums diretórios com status code <strong>200</strong>, ou seja diretórios que não precisam de autorização para acessar.</br>

```bash
200 /admin/admin.js
200 static/js/index.js
...
```

Acessei **url/admin/admin.js** e nesse arquivo estava a flag:

> "MCS{3num3r4t10n_F0rfun_4nd_Pr0f1t}"

<hr>

## Desafio: Nosferatu :triangular_flag_on_post:

<code>Formato da flag: MCS{xxxx_xxxx_xxxx_xxxx_xxxx}</code>

Continuação da análise do site.</br>

Como tinha me retornado a url <strong>static/js/index.js</strong>, acessei e retornou o diretório com a regra de negócio da aplicação. </br>

## Análise

Analisei o código **index.js**, vi que tinha requisição POST **/api/getfacts** que recebia como paramentro **(fact_type)** e retornava chamando uma const populate, passando o response.</br>
A populate continha **if else**

> if (facts.length > 0)

Na página do "button 2", não aparece o array com as informações. Caindo diretamente no **else**

```js
 facts_html = '<div></div><div class="error">Secrets can only be accessed by admin</div>';
```

Passei o body como true e rodei o scritp no console do navegador:

```js
fetch('/api/getfacts', {
  'method': 'POST',
  'headers': {
    'Content-Type': 'application/json'
  },
  'body': "{\"type\":true}"
}).then((response)=>response.json()).
    then((response)=>console.log(response));
```

![](/meninaCyberSec/pics/flga2.png)

E a flag foi retornada:

> MCS{0wn3d_fl4g_f0r_typ3_Juggl1ng}
