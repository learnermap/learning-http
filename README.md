# Aprendendo HTTP

## O que estou aprendendo?

- **19/02/2023**:

### O que é HTTP

> Hypertext Transfer Protocol

Conjunto de regras definidas para a comunicação entre duas máquinas da rede, ou seja, um cliente e um servidor.

Sendo nesse modelo o navegador representado pelo cliente e o local onde o recurso está hospedado o servidor.

O peer-to-peer é outro exemplo de protocolo, assim como o FTP e o SMTP.

### HTTPS

O HTTP é texto pura. Por isso, por todo local onde a requisição passar, será texto que estará sendo processado. 

Por essa razão, adicinou-se uma camada de segurança no HTTP chamadp SSL ou TLS.

> HTTP + TLS = HTTPS

Para um site garantir o HTTPS ele ter possuir um certificado digital de segurança. 

Um certificado deve ser assinado digitalmente por uma entidade certificadora.

Desta forma, utilizando de um par de chaves, sendo a privada no browser, para criptografar o dado, e a pública no servidor, para descriptografar o dado é que a comunicação segura ocorre.

Esse par de chaves, pública e privada, utilizada criptografia assimétrica no início da comunicação, para trocar novas chaves, agora simétricas, que serão utilizadas durante toda a comunicação.

### Endereços

Na rede, referenciamos uma máquina utilizando um endereço IP. Ex: 192.168.0.1.

Por isso, existe o DNS, que vem para resolver esse endereço, deixando-o mais amigável. Ou seja, quando digitamos algo como site.com.br, o DNS resolve esse endereços, buscando na rede o IP referente à máquina que tem esse nome, site.com.br.

O endereço omite a porta de acesso, que geralmente é padrão na porta 80, para HTTP, ou 443, no caso do HTTPS.

No endereço, url, **https:www.site.com.br:443/pagina-de-acesso**:

- https: protocolo
- www: camada de navegador, nesse caso a web.
- site.com.br: domínio, com informação da finalidade, `com`, de país, `br`.
- 443: porta, geralmente não aparece.
- pagina-de-acesso: recurso

> URL = URI ~= URL
> A URL é uma URI, mas nem toda URI é uma URL.

### Requisição x Resposta

A comunicação entre o cliente e servidor é realizada por requisição e resposta.

Basicamente, o cliente inicia com uma requisição a um recurso e o servidor, retorna com uma resposta.

Quando o cliente precisa fazer alguma identificação, enviando login e senha por exemplo, o servidor utilizada de recursos de criptografia para proteger dados sensíveis. Nesse caso, após a autenticação, o cliente não precisa mais ficar enviando dados de login a cada nova requisição, pois o servidor, possui uma tecnologia que cria uma sessão para o cliente. 

O HTTP é stateless, ou seja, não guarda estado. Assim, o cliente, a cada nova requisição é necessário se identificar ao servidor sobre suas credenciais.

Graças a tecnologia de sessão, essa identificação é realizada de forma mais simples, utilizando-se de cookies.

Cookies são utilizadas para entre outros fins, identificar ao servidor o cliente que realizou a requisição.

- **20/02/2023**:

### Depurando uma requisição

Para depurar uma requisição podemos utilizar as ferramentas de desenvolvedor presentes nos navegadores atual, F12.

Com essa ferramenta, podemos ver as requisições realizadas quando digitamos um endereço na web, e percebemos que vários outros endereços são requisitamos indiretamente, já que uma página é composta de vários outros links para ouras páginas.

Notamos também que uma forma de sinalizar o status da requisição é utilizando de códigos. Esses códigos informam ao navegador o que foi encontrado, ou qual erro foi emitido.

Por exemplo: 

```
telnet www.google.com.br
GET / HTTP/1.1
HOST: www.google.com.br

HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Vary: Accept-Encoding,User-Agent
Content-Language: pt-br
Date: Mon, 01 Jun 2015 21:00:20 GMT
Server: Google Frontend
Cache-Control: private
```

Conforme o exemplo, utilizamos o método GET para fazer a requisição, na porta 80, e recebemos o código 200 como resposta.

- Erros 

> 2xx - Successful responses
> 3xx - Redirection messages
> 4xx - Client error responses
> 5xx - Server error responses

> [HTTP Status Codes](https://www.w3schools.com/tags/ref_httpmessages.asp)
> [Status Dogs](https://httpstatusdogs.com/)

- **21/02/2023**:

### Parâmetros da requisição

Uma requisição pode conter parâmetros, por exemplo, para  que informam os dados de login de um site.

Parâmetros também são muito utilizados em pesquisas, por exemplo: 

- `https://www.site.com/results?search_query=item+procurado`
- `https://www.site.com/results?n=nome-do-item&c=cor-do-item`

Para fazer requisições, podemos utilizamos o método GET do HTTP. Esse método geralmente é utilizado para recuperar informações do servidor, e utiliza a url para enviar parâmetros.

Outra forma de fazer requisições é utilizando o método POST. Nesse caso, os parâmetros não são enviados pela url e sim, utilizando um formulário na requisição.

> Para situações de login e manipulação de dados sensíveis, a prática é sempre utilizadar o método post.

Existem outros métodos no HTTP, exemplo, DELETE, PUT e PATCH, geralmente utilizados para apagar e atualizar total e atualizar parcial.

### Serviços REST

- métodos http mais utilizados são get e post
- existem outros, exemplo, put e delete
- requisições http podem ser enviadas através de outras apps, além de navegadores.
- cabeçalhos de uma requisição auxiliam com informações adicionais na requisição, por exemplo, o formato da resposta que desejamos. 
- o HTTP envia texto puro. Por isso, em alguns casos, devemos especificar o formato que esperamos de retorno, exemplo:

`Accept: text/html, Accept: text/css, Accept: application/xml, Accept: application/json, Accept:image/jpeg e Accept: image/*`

> Os termos utilizados acima são conhecidos como MIME types.

- REST: REpresentational State Transfer, ou seja: 
  - recurso: URI
  - operações: GET/POST/PUT/DELETE
  - representação: JSON/XML/HTML

> Exemplo de serviço rest: `http://viacep.com.br/ws/13650055/json`
>
> REST é utilizar a WEB da maneira como ela foi proposta, utilizando recursos, operações e representações.


> [MIME types](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

### HTTP2

Nessa nova versão:

- os dados são trafegados em binário, ao invés de texto puro
- o header da mensagem já vem zipado por padrão, com gzip/hpack
- implementa tls por padrão.
- não é necessário enviar o header novamente, o header é stateful
- caso seja necessário alterar algo, somente o que altera é enviado no header.
- server push: envio de dados relacionados à requisições recebidos, antes do cliente solicitar.
- multiplexing: processamento paralelo de requisições, em evolução ao keep-alive da versão 1.1.
