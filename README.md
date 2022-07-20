# Boas-vindas ao repositório!

Para realizar o projeto, atente-se a cada passo descrito a seguir, e se tiver qualquer dúvida, nos envie por _Slack_! #vqv 🚀
Aqui você vai encontrar os detalhes de como estruturar o desenvolvimento do seu projeto a partir deste repositório, utilizando uma branch específica e um _Pull Request_ para colocar seus códigos.

# Termos e acordos

Ao iniciar este projeto, você concorda com as diretrizes do [Código de Conduta e do Manual da Pessoa Estudante da Trybe](https://app.betrybe.com/manual-estudante/codigo-de-etica-e-conduta).

# Mão na massa

> 🚀 Se liga nesse foguete! <br />
> Os exercícios destacados com 🚀 são os fundamentais pra você ir bem no projeto! Todos os exercícios vão contribuir com sua formação mas fique de 
> olho nesses! 👀

---
### 1. Como primeiro exercício, vamos usar a função `fetch`, que vimos na aula ao vivo, para criar um site simples com um gerador de piadas ruins!. Como? Vamos praticar!

> Primeiro, veja o [manual da API do site icanhazdadjoke.com.](https://icanhazdadjoke.com/api) Ele esclarece como fazer as requisições ao serviço de 
> piadas. Por hora, pode só passar o olho; agora vamos entender como funciona essa API:

  - Para começar, vamos fazer uma requisição via browser. Visite o site [icanhazdadjoke.com](https://icanhazdadjoke.com/api), e perceba que ele devolve uma página HTML com uma piada aleatória.
Em seguida, no terminal, vamos fazer a requisição: `curl -H "Accept: text/html"` "[https://icanhazdadjoke.com/](https://icanhazdadjoke.com/)". Perceba que o retorno é um HTML idêntico ao de uma requisição via browser com uma piada aleatória.

  - Para a próxima requisição, vamos usar o comando: `curl -H "Accept: text/plain"` "[https://icanhazdadjoke.com/](https://icanhazdadjoke.com/)". Veja que agora recebemos apenas a piada aleatória em formato texto.

  - Por fim, faça a requisição: `curl -H "Accept: application/json"` "[https://icanhazdadjoke.com/](https://icanhazdadjoke.com/)". Agora a API retorna um objeto no formato `JSON.
Perceba que, dependendo do que passamos na chave `Accept:` no header, definido por `-H` no comando, o serviço nos retorna uma resposta diferente.

- Utilize o `HTML` e o `js` já criado nesse repositório 
-  Não se esqueça de utilizar a extensão <strong>Live Server</strong> e inspecionar o `console` do navegador para ver os `logs`

<details>
  <summary><strong>Arquivo já existente no projeto <code>jokes.html</code> </strong></summary><br />

```
<!DOCTYPE html>
<html>
  <head>
    <title>Best jokes ever</title>
    <script src="apiScript.js" ></script>
  </head>
  <body>
    <h1>Get ready for a great joke!</h1>
    <h2 id="jokeContainer"></h2>
  </body>
</html>
```
</details>

  <details>
    <summary><strong>Arquivo já existente no projeto <code>apiScript.js</code> </strong></summary><br />

  ```
  const API_URL = 'https://icanhazdadjoke.com/';

  const fetchJoke = () => {
    // Adicionar lógica aqui!
  };

  window.onload = () => fetchJoke();
  ```
  </details>

<details>
  <summary>O que será verificado</summary><br />

  - Será valiado, se está sendo criado um objeto com uma variável `fetchJock`
  - Será valiado, se esse objeto está usando `method` e `headers`
  - Será valiado, se está utilizando `fetch` consumindo a variável `API_URL`
</details>

---

### 2 . Agora vamos tentar fazer as requisições a API usando `fetch`. Essa função recebe dois parâmetros

- O endereço para o qual a requisição será feita, ou seja, a url do serviço.
- Um objeto contendo as especificações da requisição. Para essa `API`, atribuiremos a esse objeto as chaves `method` e `headers`

<details>
  <summary><strong> De olho na dica 👀 </strong></summary><br />

```
const fetchJoke = () => {
  const myObject = {
    method: 'GET',
    headers: { 'Accept': 'application/json' }
  };

  fetch(API_URL, myObject);
};
```
</details>

- O segundo parâmetro `myObject` define o tipo de request: `method: 'GET'` e o formato da resposta `headers: { 'Accept': 'application/json' }`, como visto nas requisições via `curl` .

  - A função `fetch` <strong>é uma Promise </strong> (você não precisa entender o que é uma Promise agora, considere apenas como sendo algo assíncrono) e, como tal, dependendo de seus desdobramentos, podemos encadear procedimentos a serem feitos, utilizando as cláusulas `.then`(em caso de sucesso) e `.catch`(em caso de falha). A requisição `fetch` retorna um objeto Response. Utilizando `.then`, verifique a estrutura da resposta usando um `console.log` na `response` retornada pelo `fetch`.

<details>
  <summary><strong> De olho na dica 👀 </strong></summary><br />

```
  fetch(API_URL, myObject)
    .then(response => console.log(response));
```
</details>

  - Viu a response? Até recebemos uma resposta do serviço, mas como é que eu consigo retirar o texto da piada daí 🤔?
  
- Para isso, usamos o método `.json()` na resposta da API. Esse método converte o conteúdo do `body` da Response e retorna uma outra Promise, que, quando bem-sucedida, retorna um JSON contendo as informações da piada.

- A partir do `fetch`, troque o `console.log()` anterior pelo método `.json()` e imprima os dados da requisição.

<details>
<summary><strong> De olho na dica 👀 </strong></summary><br />

```
  fetch(API_URL, myObject)
    .then(response => response.json())
    .then(data => console.log(data));
```
</details>

- Recebemos um objeto, certo? A partir daí, faça a piada aparecer no `DOM` da sua página!

---

### 3 . Agora vamos tentar fazer as requisições a API usando `fetch`. Essa função recebe dois parâmetros
- Vamos consultar uma `API` que fornece os valores de crypto moedas e mostrar as 10 primeiras.
A documentação para a `API` que vamos utilizar esta disponível nesse [link](https://docs.coincap.io/).
  - Tente descobrir qual url vamos utilizar para buscar as informações que precisamos (um `array` com uma listagem das crypto moedas).
Se ficou na dúvida veja a seguir <strong>(spoiler alert!)</strong>

<details>
<summary><strong> De olho na dica 👀 </strong></summary><br />

```
url: `https://api.coincap.io/v2/assets`
```
</details>


- Por se tratar de uma API pública a quantidade de requisições a ela é limitada, caso você se depare com o seguinte erro: `FetchError: invalid json response body at (url da API) reason: Unexpected token T in JSON at position 0`, significa que você foi bloqueado temporariamente, basta esperar 1 ou 2 minutos para poder voltar a usar normalmente.
  - Agora que temos a url vamos criar um arquivo (`api.js`, por exemplo) e dentro dele uma função para pegar o array com as moedas.
  
  - Crie também um arquivo HTML (`index.html`, por exemplo) que deve conter uma tag para listar as crypto moedas.
  
  - 🚀 Pronto, temos um `array` com os dados das moedas e um esqueleto do HTML, agora vamos fazer com que as moedas apareçam na tela. Utilize o seguinte formato: `Nome da moeda (símbolo da moeda): valor em dólares`. Exemplo: `Bitcoin (BTC): 46785.06`.
  
  - 🚀 Conseguiu mostrar as moedas na tela? Agora, que tal usar uma Higher Order Function para filtrar o `array das moedas para mostrar apenas as 10 primeiras?
  
  - Não se esqueça de estilizar a página conforme o seu estilo (tanto no CSS quanto no HTML).

---  
# Requisito bônus
### 4 . Que tal usarmos uma API para converter o preço das crypto moedas do exercício anterior para a nossa moeda local ao invés de mostrar o seu valor em dólar?
- Para este exercício vamos utilizar a `Currency API`. Tente descobrir qual url retorna os dados necessários para este exercício, mas caso fique na dúvida pode consultar a informação abaixo:

<details>
  <summary><strong> URL (spoiler alert!) </strong></summary><br />

```
  baseUrl: `https://cdn.jsdelivr.net/gh/fawazahmed0/currency-api@1/latest`
  endpoint: `/currencies/usd.min.json`
```
</details>



