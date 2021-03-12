# Code Challenge Yungas Full Stack

O objetivo deste desafio é avaliar a sua maneira de pensar e resolver os problemas propostos.

A forma como você resolverá este desafio é importante para entendermos seus padrões de qualidade, organização, performance, etc. Além dos requisitos que serão citados, diversos outros serão também avaliados (mas esses são surpresa, ok?)

No final, lhe daremos retorno sobre os pontos que achamos positivos e negativos.

A Yungas usa um stack de transição e híbrido com Flask/Jinja/JQuery e módulos mais atuais onde o frontend é Svelte com chamadas REST. Não tem problema não estar familiarizado com Svelte se você for frontend, se você teve experiência com Vue ou React, Svelte será moleza pra você.

Para este desafio, recomendamos que utilize o stack Flask+Svelte (especialmente o Flask). No front, preferimos que evite utilizar bibliotecas de componentes - afinal, queremos ver o seu código e a sua maneira de resolver problemas.

**Tenha certeza de que seu código foi testado (inclusive testes automatizados vão lhe dar pontos extras) e está pronto para rodar!**

Consideramos diferenciais (positivos):
- Projetos organizados.
- Código limpo.
- Composition over inheritance.
- Declarativo sobre imperativo.
- Caso sênior, comentários (pode ser no README) sobre como faria deploy deste app (configs, adições ao stack, etc). Quanto mais detalhes, melhor!

---

# BACKEND

Seu desafio no backend será criar uma API que listará pessoas de uma base de dados.

Neste repositório você encontrará o arquivo **people.json**. Você deve usar este arquivo como sua base de dados importando-o para um banco de dados, para uma variável, tanto faz. O importante é que isto ocorra durante a inicialização do seu projeto.

Exemplo do JSON:
```
{"gender":"male","name":{"title":"mr","first":"antonelo","last":"da conceição"},"location":{"street":"8986 rua rui barbosa ","city":"santo andré","state":"alagoas","postcode":40751,"coordinates":{"latitude":"-69.8704","longitude":"-165.9545"},"timezone":{"offset":"+1:00","description":"Brussels, Copenhagen, Madrid, Paris"}},"email":"antonelo.daconceição@example.com","dob":{"date":"1956-02-12T10:38:37Z","age":62},"registered":{"date":"2005-12-05T15:22:53Z","age":13},"phone":"(85) 8747-8125","cell":"(87) 2414-0993","picture":{"large":"https://randomuser.me/api/portraits/men/8.jpg","medium":"https://randomuser.me/api/portraits/med/men/8.jpg","thumbnail":"https://randomuser.me/api/portraits/thumb/men/8.jpg"}}
```

## Especificações da API

### Requisito #1

A API deve sempre responder com paginação e todas as saídas da API devem ser padronizadas no seguinte formato:

```
{
  page: X,
  page_size: Y,
  total_items: T,
  items: [ ... ]
}
```

Ou seja, todos os endpoints de sua API devem aceitar os parâmetros **page** e **page_size** e formatar a saída de acordo, informando que página esta sendo exibida, qual é o número máximo de itens por página e o número total na base de dados.


### Requisito #2

Você notará que todos os usuários de sua base de dados estão localizados em estados brasileiros e os usuários de sua API precisam listá-los por região. Faça com que sua API possua rotas onde o usuário possa passar a região e receber a lista filtrada de usuários daquela região: Lembrando que as regiões disponíveis serão:
- Norte
- Nordeste
- Centro-Oeste
- Sudeste
- Sul


### Requisito #3

Você sabe que sua API fará muito sucesso em breve e você vai atingir fama internacional. Pensando nisto, você já está adaptando a saída da API para algo mais genérico para o mercado internacional. Para melhorar a saída da API você precisa:

1. Os números de telefone devem estar no formato [E.164](https://en.wikipedia.org/wiki/E.164). Por exemplo, (44) 4422-3311 será convertido para +554444223311.
2. Inserir a nacionalidade. Como todos os clientes ainda são do Brasil, o valor padrão será BR.
3. Alterar o valor do campo `gender` para `F` ou `M` em vez de `female` ou `male`.
4. Retirar o campo `age` de `dob` e `registered`.
5. Alterar estrutura para simplificar leitura e usar arrays em campos específicos (ver exemplo abaixo)

Exemplo de OUTPUT:

```
{
  "gender": "m",
  "name": {
    "title": "mr",
    "first": "quirilo",
    "last": "nascimento"
  },
  "location": {
    "region": "sul"
    "street": "680 rua treze ",
    "city": "varginha",
    "state": "paraná",
    "postcode": 37260,
    "coordinates": {
      "latitude": "-46.9519",
      "longitude": "-57.4496"
    },
    "timezone": {
      "offset": "+8:00",
      "description": "Beijing, Perth, Singapore, Hong Kong"
    }
  },
  "email": "quirilo.nascimento@example.com",
  "birthday": "1979-01-22T03:35:31Z",
  "registered": "2005-07-01T13:52:48Z",
  "telephoneNumbers": [
    "+556629637520"
  ],
  "mobileNumbers": [
    "+553270684089"
  ],
  "picture": {
    "large": "https://randomuser.me/api/portraits/men/83.jpg",
    "medium": "https://randomuser.me/api/portraits/med/men/83.jpg",
    "thumbnail": "https://randomuser.me/api/portraits/thumb/men/83.jpg"
  },
  "nationality": "BR"
}

```
**Os dados devem ser armazenados conforme o contrato de OUTPUT também.**

---

# FRONTEND
Já no frontend, seu desafio é exibir os dados da API criada.

Neste repositório, você encontrará um arquivo chamado **people.json**. Ele será sua base de dados. Faça um mock de uma API e receba os dados através dela. Com os dados, você deve atender os requisitos abaixo.

### Requisito #1

Você deve criar uma interface que liste todos os registros. Esta interface deve conter formas de filtragem e organização dos dados como:
- filtros por partes dos dados, como nome, endereco, cidade, etc.
- organizacao dos registros por ordem alfabetica ou inversa.
- o estado default da tela é lista completa, sem filtragens.

### Requisito #2

Você notará que todos os usuários de sua base de dados estão localizados em estados brasileiros mas na sua interface, precisamos listá-los por região. Crie também um filtro com um SELECT onde se possa selecionar as regiões abaixo e filtrar os registros listando apenas estados pertencentes aquela regiao
- Norte
- Nordeste
- Centro-Oeste
- Sudeste
- Sul

### Requisito #3

A sua interface precisa listar no máximo 20 usuários por vez, possuir paginação e identificar quando é necessário exibir os controles de paginação. A paginação deve conter botões para ir para a primeira ou última página, avançar ou retroceder uma página e também um local onde o usuário pode digitar diretamente a página que ele quer exibir.

### Requisito #4

Sua interface deve ser responsiva.

### Requisito #5 

Seus filtros devem ser INCREMENTAIS, ou seja, se você filtrar por "Joao" e região "Sul", somente os "Joao" da região "Sul" devem ser exibidos. Se outro filtro for adicionado a busca, ele também precisa incrementar a pesquisa.

### Requisito #6

Ao clicar em uma pessoa da listagem, esta pessoa deve ser exibida em um modal com mais detalhes. Pontos aqui se você for mais criativo e não usar um modal, apresentando os dados de outra forma e que tenha uma boa UX.

# Como entregar

Crie seu repositório no Github e o mantenha como **privado**!!

Dê permissão de acesso para [@k-onrad](https://github.com/k-onrad) ao seu repositório.

É obrigatório ter um **README** com todas as instruções sobre o seu desafio.

Assim que finalizar, nos avise pelo e-mail marcos@yungas.com.br para que possamos avaliar.

## Boa sorte!
