# Aprendendo HTTP

## O que estou aprendendo?

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






### 
