# Simulando-um-Ataque-de-Brute-Force-de-Senhas
Implementar, documentar e compartilhar um projeto prático utilizando Kali Linux or Parrot OS e a ferramenta Medusa, ncrack, Hydra, BurpSuite em conjunto com ambientes vulneráveis (por exemplo, Metasploitable 2 e DVWA), para simular cenários de ataque de força bruta e exercitar medidas de prevenção.

## Configurações de rede do alvo
<img width="1365" height="767" alt="1" src="https://github.com/user-attachments/assets/76a2e532-201d-499a-b720-706e8fcd76eb" />

## Teste de conectividade usando o utilitário de rede ping.
<img width="1365" height="767" alt="2" src="https://github.com/user-attachments/assets/9d56fb32-c858-4af4-815d-3073aa2e188d" />

## Criando a lista de senhas e usúarios personalizada 
Nota: A mesma lista será utilizada para realizar o ataque de força-bruta na aplicação Web do DVWA


<img width="1365" height="767" alt="4" src="https://github.com/user-attachments/assets/086862ad-521a-47c5-97b5-6beaf8391ff1" />

## Realizei um ataque de brute-force no serviço FTP (FILE TRANSFER PROTOCOL) usando o ncrack. 
Nota: A ferramenta encontrou uma combinação de username e password - *Credenciais.*

Mindset Hacker: Podemos executar uma ataque de Credentials Stuffing para tentar entrar em outros serviços com o mesmo username (usúario) ou senha


<img width="1365" height="767" alt="5" src="https://github.com/user-attachments/assets/61dd7651-988e-4108-88a1-3384e3277760" />


## Depois que o ataque *Credentials Stuffing* foi executado, encontramos o username e passoword para realizar o login usando o ssh (secure shell) na porta padrão 22.
<img width="1365" height="727" alt="7" src="https://github.com/user-attachments/assets/6e22cfa3-b8ce-40fe-ab94-7d76f3a43296" />


## Na enumeração, a porta 80 (http) foi considerada como open - aberta. 
Podemos usar a ferramenta cli **curl** para verificar se existe arquivos interesantes ou formulários...
<img width="1365" height="794" alt="8-curl-part1" src="https://github.com/user-attachments/assets/04f2651e-0873-40f9-9784-458d8659151d" />


- A resposta à nossa solicitação foi 200 (OK), e obtivemos informações adicionais no corpo da resposta HTTP.
Podemos observar que o método HTTP utilizado foi GET, o conteúdo retornado corresponde ao código-fonte HTML da página, e o alvo acessado foi o host especificado.


## Part2 - OUTPUT do request - "CURL"
<img width="1365" height="767" alt="8-curl-part2" src="https://github.com/user-attachments/assets/46a8444a-cf3c-41e4-8c18-23b94562c810" />

Podemos notar que o *Host*  tem hiperlinks ou caminhos para outras páginas dentro do site **http://192.168.192.129.**

## Na enumeração, também encontramos a porta 21 marcada como open.
Vamos realizar uma tentiva de login usando as credenciais fornecidas previamente pela a ferramenta ncrack.

<img width="1365" height="767" alt="9-ftp-part1" src="https://github.com/user-attachments/assets/94925dc3-b3a1-4a04-97f2-a4b62df615c3" />


 - Observe que tivemos êxito na autenticação. Temos um nivel de autorização considerado alto, pois, consiguimos acessar a pasta "/home" de forma muito fácil.
Será que tem arquivos na pasta "/home/msfadmin"?

- Não encontramos arquivos, porém existe um diretório com permissões inseguras.
- O proprietário possui permissões de leitura (r), escrita (w) e execução (x). Já os usuários convidados ou outros têm apenas permissão de execução (x).
- Isso significa que podemos entrar no diretório, mas não podemos criar (escrever) nem ler arquivos.


<img width="1365" height="767" alt="9-ftp-part2" src="https://github.com/user-attachments/assets/971f5fc4-16bf-4f3e-a7ab-b62855234abb" />

## Ataque de Brute-Force em formúlarios Web do alvo usando o BurpSuite Community.

 Interceptei uma request (solicitação) de tentativa de login no site do alvo.
 
<img width="1365" height="767" alt="10-Bforceweb-part1" src="https://github.com/user-attachments/assets/cfca2bd0-5e79-487a-b439-35b7c4560f42" />

__

No print abaixo, estou simulando um ataque de força bruta contra um ambiente vulnerável utilizando o **Burp Suite Community Edition**. A aplicação-alvo é o **DVWA (Damn Vulnerable Web Application)**, hospedada em `http://192.168.192.129/dvwa/login.php`.

No lado esquerdo da tela, configurei uma requisição **HTTP POST** no Burp Suite, enviando credenciais de login (`username=admin&password=admin`) para testar a resposta do servidor. A requisição inclui cabeçalhos padrão como `Content-Type: application/x-www-form-urlencoded`, `User-Agent`, `Referer` e outros que simulam o comportamento de um navegador legítimo.

À direita, estou documentando o processo em um terminal com editor de texto aberto. Nele, a notei as combinações de username e password - a lista de **payloads de usuário e senha** que serão utilizados no ataque de força bruta. Essa lista inclui combinações comuns como `admin`, `1234`, `admin1`, `admin2`, `teste`, entre outras.

O objetivo deste teste é verificar se o sistema possui mecanismos de proteção contra tentativas automatizadas de login, como bloqueio por IP, CAPTCHA ou limitação de requisições. Até o momento, o ambiente se mostrou vulnerável, permitindo múltiplas tentativas sem restrições aparentes.
--

<img width="1365" height="767" alt="10-Bforceweb-part2" src="https://github.com/user-attachments/assets/04bd3367-8363-4686-9831-5c5cc62c1dac" />

>
>

No print abaixo, estou utilizando o **Burp Suite Community Edition** para realizar testes de segurança em uma aplicação vulnerável, o **DVWA (Damn Vulnerable Web Application)**, acessível em `http://192.168.192.129/dvwa/login.php`.

O foco principal está no módulo **Repeater**, onde estou manipulando e reenviando uma requisição **HTTP POST** para o endpoint de login da aplicação. Essa funcionalidade do Burp Suite permite testar manualmente diferentes combinações de parâmetros e observar como o servidor responde a cada tentativa.

A requisição enviada inclui os seguintes cabeçalhos:

```
POST /dvwa/login.php HTTP/1.1
Host: 192.168.192.129
Content-Length: 29
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.192.129
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/117.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Referer: http://192.168.192.129/dvwa/login.php
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.5
Connection: close
```

No corpo da requisição, estou testando as credenciais:

```
username=admin&password=admin
```

O **Repeater** é essencial para este tipo de análise, pois me permite modificar os parâmetros de forma rápida e observar a resposta HTTP da aplicação em tempo real. Com isso, consigo identificar padrões de resposta, mensagens de erro, e potenciais falhas de autenticação que podem ser exploradas em ataques mais avançados, como `força bruta`.

<img width="1365" height="767" alt="10-Bforceweb-part3" src="https://github.com/user-attachments/assets/a9edbbc6-97b5-4c92-8c3c-bb73a9ffa474" />



---


<img width="1365" height="767" alt="10-Bforceweb-part4" src="https://github.com/user-attachments/assets/be56d37b-36f6-40d0-b4d6-d5c3a9c13cc5" />


Neste momento do projeto, estou utilizando  o módulo **Repeater**, para realizar testes manuais de autenticação na aplicação vulnerável.

No lado esquerdo do print, o Burp Suite exibe uma requisição **HTTP POST** que estou manipulando diretamente no Repeater. Essa requisição é enviada para o endpoint `/dvwa/login.php`, e contém os seguintes parâmetros no corpo:

```
username=msfadmin&password=naftali&Login=Login
```

Os cabeçalhos da requisição foram mantidos conforme o navegador original, simulando uma tentativa legítima de login:

```
POST /dvwa/login.php HTTP/1.1
Host: 192.168.192.129
Content-Length: 44
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://192.168.192.129
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/117.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8
Referer: http://192.168.1.10/dvwa/login.php
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.5
Connection: close
```

O **Repeater** é uma ferramenta essencial para esse tipo de análise, pois me permite modificar os parâmetros da requisição — como o nome de usuário, senha ou até mesmo o campo `Login` — e reenviar rapidamente para observar como o servidor responde. Isso facilita a identificação de padrões de resposta, mensagens de erro específicas e possíveis brechas no mecanismo de autenticação.

No lado direito do print, o navegador exibe a interface da DVWA com o formulário de login. Após o envio da requisição manipulada, a aplicação retorna a mensagem **"Login failed"**, indicando que as credenciais testadas não foram aceitas. Essa resposta é útil para validar o comportamento da aplicação diante de diferentes combinações de usuário e senha.

Esse processo é parte da fase de **reconhecimento e enumeração de falhas**, onde busco entender como a aplicação trata entradas inválidas e se há espaço para ataques como **força bruta** ou **bypass de autenticação**.

>
>

- A resposta da solicitação. O Status code foi `302 Found` isso indica que ocorreu falha no login...
- Vamos automatizar usar `Intruder` para realizar o ataque de brute-force.
<img width="1365" height="767" alt="10-Bforceweb-part5" src="https://github.com/user-attachments/assets/3580a134-525e-4ba4-b1ea-8f54b07f088f" />

>

OBS: Esqueci de tira prints da configuração dos payloads e suas posições.

<img width="1365" height="767" alt="10-Bforcewebintruder-part5" src="https://github.com/user-attachments/assets/0d37d9f8-057d-43fe-b6e2-f7be1da80d7a" />

- Na imagem, podemos ver no lado direito que o `Intruder Attack` que realizei foi direcionado para a URL ```http://192.168.192.129```.
- Já no lado esquerdo podemos ver que a aplicação retornou ```You have logged in as 'admin'```. Com essa informação podemos ter a certeza que o usúario é admin.
- E podemos tentar um login com o ```Payload 2``` que contém o valor  **password** na segunda solicitação ou request 2.

>
>
 ## USER and PASS FOUND !!!
<img width="1365" height="767" alt="10-Bforcewebintruder-part6" src="https://github.com/user-attachments/assets/d5a79fab-5da8-45f2-a477-78faa7c78df5" />

>
#  **Security Level** 


>

A aplicação Web estava com o nível de segurança (**Security Level**) medium ou médio.

<img width="1365" height="767" alt="10-Bforcelevel" src="https://github.com/user-attachments/assets/5e8fee9c-74a2-4dca-b7eb-407da343beb7" />


>
## Considerações Finais:
- Esse foi um projeto simulando não apenas, um ataque de brute-force, mas diversos ataques em ambiente ético e autorizado por mim, @NaftalidaCosta.
- É importante o conhecimento, o Santander e a DIO promovem bootcamps em diversas áreas. Esse projeto foi realizado durante a fase de Desafio de Projeto do Bootcamp **Santader - Cibersegurança 2025**.
- Como estudante de Tecnologia da Informação sou grato por participar dos Bootcamps do Santander & Dio e realizar os desafios de todos os bootcamps.
- Atensiosamente, Naftali da Costa.

