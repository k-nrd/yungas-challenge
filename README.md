# Code Challenge Yungas Back-end

O objetivo deste desafio é avaliar a sua maneira de pensar e resolver os problemas propostos.

A forma como você resolverá este desafio é importante para entendermos seus padrões de qualidade, organização, performance, etc. No final, lhe daremos retorno sobre os pontos que achamos positivos e negativos.

Utilize nesse desafio os frameworks que mais dominar, mas preferimos *fortemente* que evite soluções prontas (Generic Views, OpenAPI codegen) - afinal, queremos ver o seu código e a sua maneira de resolver problemas.

Must-have:
- Projeto organizado.
- Código limpo.
- Back-end com estrutura clara e responsabilidades bem definidas.
- Rotas documentadas (como utilizar, o que enviar, etc).
  - Obs.: Nesse ponto específico, pode usar soluções que automatizem o processo.

Nice-to-have (não é "tudo ou nada", faça o que conseguir!):
- Containerização.
- Testes unitários.
- Código funcional ao invés de orientado a objetos.
- Código declarativo ao invés de imperativo.
- Comentários (pode ser no README) sobre como faria deploy deste app. Como lidaria com:
  - Configs?
  - Secrets?
  - Logs?
  - Quanto mais detalhes, melhor!
- Deploy deste app na AWS ou Heroku (mas não precisa gastar dinheiro!).

---

## O DESAFIO

Seu desafio será criar um sala de chat em tempo real. Para isso, use websockets ou um protocolo similar como socket.io. 
Você pode apenas documentar as rotas implementadas ou criar um front-end mínimo para utilização das rotas. Faça como preferir, o importante é a funcionalidade do back.

Temos requerimentos de diferentes níveis para devs com diferentes níveis de experiência. Mesmo se for experiente, não pule níveis. Tente finalizar um nível antes de seguir ao próximo. Dentro de um nível, no entanto, pode fazer os itens na ordem que preferir!

### Requerimentos mínimos
- Implementar rotas de websocket ou socket.io.
- Definir uma sala de chat padrão (pode chamar de Sala 1).
- Usuários devem entrar na sala de chat com o username que escolherem.
- Enviar ao usuário que entrou na sala uma lista dos usuários presentes na sala.
- Recusar mensagens enviadas por usuários que não estão na sala.
- Notificar todos os outros usuários quando um usuário novo entrar na sala.
- Notificar todos os outros usuários quando receber mensagens de algum dos usuários da sala.
- Notificar todos os outros usuários quando um usuário da sala estiver digitando.
- Notificar todos os outros usuários quando um usuário da sala que estava digitando parar de digitar.
- Notificar todos os outros usuários quando um usuário da sala sair da sala.

### Requerimentos intermediários
- Definir mais salas (Sala 2 e Sala 3, por exemplo).
- Usuários só podem estar em uma sala por vez.
- Usuários que estão em uma sala não podem ver mensagens de outras salas.
- Notificar todos os outros usuários da sala quando um usuário da sala começar a digitar uma mensagem.
- Notificar todos os outros usuários da sala quando um usuário da sala parar de digitar.

### Requerimentos avançados
- Faça com que o usuário se registre ou faça login para entrar em uma sala.
- A autenticação pode ser implementada da maneira que preferir (JWT, Basic Auth, etc). Procure usar uma library popular para o framework que escolheu.
- `nome`, `username`, `senha` (encriptada, claro) e `email` devem ser persistidos em um banco de dados SQLite.
- Implementar sessões, de tal maneira que o usuário não precise refazer o login quando der um refresh ou fechar e abrir a aba.
- A implementação das sessões, assim como da autenticação, fica a seu critério (pode usar uma library que faça ambos).
- Implementar uma rota HTTP que deve:
  - Receber arquivos via FormData (o texto da mensagem ainda deve ir via socket, mas deve esperar o envio dos arquivos).
  - Salvar os arquivos em uma pasta local `/tmp`.
  - Retornar links para esses arquivos (o backend deve servir esses arquivos em `/static/<NOME-DO-ARQUIVO>`).
  - Obs.: No caso de mais de um arquivo, lembre de retornar um array de links.
  - Obs2.: Arquivos podem demorar para serem recebidos e operações I/O para salvar no disco podem ser lentas - recomendamos que utilize `async` ao máximo.

## Como entregar

Crie um repositório no Github. O repositório deve ser privado enquanto não te avaliamos, mas depois da avaliação pode deixar público e utilizar para portfólio se quiser!

Dê permissão de acesso para [@kvdos-argonaut](https://github.com/kvdos-argonaut) ao seu repositório.

É **obrigatório** ter um **README** com todas as instruções para rodar o seu desafio (podem ser comandos `python` e `npm`/`yarn`, comandos `docker` ou `docker-compose` se você containerizou o app ou até mesmo um link para o heroku/aws/host de sua preferência com o app rodando).

Assim que finalizar, envie um link para o repositório para o e-mail `marcos@yungas.com.br`, para que possamos avaliar.

## Precisa de referências?
Dẽ uma olhada nesses links:
- https://flask-socketio.readthedocs.io/en/latest/getting_started.html
- https://fastapi.tiangolo.com/advanced/websockets/
- https://sanicframework.org/en/guide/advanced/websockets.html
- https://svelte.dev/tutorial/basics
- https://www.valentinog.com/blog/socket-react/
- https://github.com/kvdos-argonaut/polka-chat
- https://github.com/scottdomes/svelte-chat

## Boa sorte!
