# Simulando-um-Ataque-de-Brute-Force-de-Senhas
Implementar, documentar e compartilhar um projeto prático utilizando Kali Linux or Parrot OS e a ferramenta Medusa, ncrack, Hydra, BurpSuite em conjunto com ambientes vulneráveis (por exemplo, Metasploitable 2 e DVWA), para simular cenários de ataque de força bruta e exercitar medidas de prevenção.

## Configurações de rede do alvo
<img width="1365" height="767" alt="1" src="https://github.com/user-attachments/assets/76a2e532-201d-499a-b720-706e8fcd76eb" />

## Teste de conectividade usando o utilitário de rede ping.
<img width="1365" height="767" alt="2" src="https://github.com/user-attachments/assets/9d56fb32-c858-4af4-815d-3073aa2e188d" />

## Criando a lista de senhas e usúarios personalizada 
Nota: A mesma lista será utilizada para realizar o ataque de força-bruta na aplicação Web do DVWA


<img width="1365" height="767" alt="4" src="https://github.com/user-attachments/assets/086862ad-521a-47c5-97b5-6beaf8391ff1" />

## Realizei um ataque de brute-force no serviço ftp usando o ncrack. 
Nota: A ferramenta encontrou uma combinação de username e passoword - *Credenciais.*

Mindset Hacker: Podemos executar uma ataque de Credentials Stuffing para tentar entrar em outros serviços com o mesmo username (usúario) ou senha


<img width="1365" height="767" alt="5" src="https://github.com/user-attachments/assets/61dd7651-988e-4108-88a1-3384e3277760" />


## Depois que o ataque *Credentials Stuffing* foi executado, encontramos o username e passoword para realizar o login usando o ssh (secure shell) na porta padrão 22.
<img width="1365" height="727" alt="7" src="https://github.com/user-attachments/assets/6e22cfa3-b8ce-40fe-ab94-7d76f3a43296" />


## Na enumeração a porta 80 (http) foi considerada como open - aberta. 
Podemos usar a ferramenta cli **curl** para verificar se existe arquivos interesantes ou formulários...
<img width="1365" height="794" alt="8-curl-part1" src="https://github.com/user-attachments/assets/04f2651e-0873-40f9-9784-458d8659151d" />
A resposta da nossa solicitação foi 200 (OK) e obtive mais informações no corpo da resposta http.
Acima podemos ver que o metodo http usado foi o ""GET"", código "HTML" ou o source code da página, e o alvo alcançado - Host. 

## Part2 - OUTPUT do request - "CURL"
<img width="1365" height="767" alt="8-curl-part2" src="https://github.com/user-attachments/assets/46a8444a-cf3c-41e4-8c18-23b94562c810" />
Podemos notar que o *Host*  tem hiperlinks ou caminhos para outras páginas dentro do site **http://192.168.192.129.**








