# Code Challenge Yungas Full Stack

O objetivo deste desafio é avaliar a sua maneira de pensar e resolver os problemas propostos.

A forma como você resolverá este desafio é importante para entendermos seus padrões de qualidade, organização, performance, etc. No final, lhe daremos retorno sobre os pontos que achamos positivos e negativos.

A Yungas usa um stack de transição com back-end em Flask e:
- front-end em Jinja+jQuery nos módulos mais antigos;
- front-end Svelte nos módulos mais novos. 

Familiaridade com Svelte não é um requerimento, mas um diferencial. Se você teve experiência com Vue ou React, Svelte será moleza pra você.

Utilize nesse desafio os frameworks que mais dominar, mas preferimos *fortemente* que evite soluções prontas tanto no back quanto no front (Generic Views, OpenAPI codegen, libraries de componentes prontos) - afinal, queremos ver o seu código e a sua maneira de resolver problemas.

Must-have:
- Projeto organizado.
- Código limpo.
- Front-end com componentes simples e reutilizáveis.
- Back-end com estrutura clara e responsabilidades bem definidas.

Nice-to-have (não é "tudo ou nada", faça o que conseguir!):
- Containerização.
- Testes unitários.
- Código funcional ao invés de orientado a objetos.
- Código declarativo ao invés de imperativo.
- Composition ao invés de inheritance.
- Comentários (pode ser no README) sobre como faria deploy deste app. Como lidaria com:
  - Configs?
  - Secrets?
  - Logs?
  - Quanto mais detalhes, melhor!
- Deploy deste app na AWS ou Heroku (mas não precisa gastar dinheiro!).

---

## O DESAFIO

Seu desafio será criar um sala de chat em tempo real. Para isso, use websockets ou um protocolo similar como socket.io. Quando estiver em dúvida sobre estilização ou estética em geral, use WhatsApp ou Telegram como referências - ambos possuem interfaces simples e intuitivas (sem exagero! Não precisamos de foto de perfil ou fundos customizáveis, haha).

Temos requerimentos de diferentes níveis para devs com diferentes níveis de experiência. Mesmo se for experiente, não pule níveis. Tente finalizar um nível antes de seguir ao próximo. Dentro de um nível, no entanto, pode fazer os itens na ordem que preferir!

### Requerimentos mínimos
- Back-end:
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
- Front-end:
  - Pedir ao usuário um username para que ele possa entrar na sala.
  - Implementar, de maneira componentizada:
    - Um menu com a lista de usuários ativos.
    - Um menu com a lista de salas.
    - Uma lista de mensagens (a parte principal de um chat, haha).
    - Uma área para digitar mensagens, com um botão para enviar mensagens.
  - Utilizar os componentes para montar o chat.
  - Notificar ao back-end quando entrar na sala.
  - Notificar ao back-end quando sair da sala.
  - Notificar ao back-end ao enviar uma mensagem (pode ser via clique em um botão escrito `Enviar`, por exemplo).
  - Quando for notificado pelo back-end, mostrar ou atualizar uma lista de usuários ativos na sala.
  - Quando for notificado pelo back-end, atualizar a lista de usuários ativos na sala.
  - Quando for notificado pelo back-end, mostrar no chat a mensagem recebida (diferenciar mensagens próprias de uma mensagem de outro usuário) e fazer um auto-scroll para baixo (para que o usuário não tenha que dar scroll manualmente).

### Requerimentos intermediários
- Back-end:
  - Definir mais salas (Sala 2 e Sala 3, por exemplo).
  - Usuários só podem estar em uma sala por vez.
  - Usuários que estão em uma sala não podem ver mensagens de outras salas.
  - Notificar todos os outros usuários da sala quando um usuário da sala começar a digitar uma mensagem.
  - Notificar todos os outros usuários da sala quando um usuário da sala parar de digitar.
- Front-end:
  - Implementar alguma maneira de trocar de salas (pode ser em abas ou menus laterais).
  - Implementar interface para login ou registro do usuário (antes de entrar em uma sala).
  - Mensagens das salas *não devem aparecer* para usuários não-autenticados.
  - Mostre as informações extras do usuário (nome e email) em algum lugar da tela (um modal que abre ao clicar no usuário na lista, por exemplo).
  - Quando for notificado pelo back-end, mostrar em algum lugar na tela qual usuário está digitando (algo como `João is typing...`).
  - Quando for notificado pelo back-end, parar de mostrar que aquele usuário está digitando (se João parar de digitar, mas Pedro continua digitando, mostrar `Pedro is typing...`).

### Requerimentos avançados
- Back-end:
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
- Front-end:
  - Ajustar a interface para permitir que arquivos sejam enviados (pode ser um botão `Anexar` ao lado de `Enviar`, por exemplo).
  - Enviar os arquivos via para a rota de upload (não envie o texto da mensagem!).
  - Uma vez que os arquivos sejam enviados, envie junto do texto da mensagem o array de links que recebeu na response.
    - Obs.: Se a mensagem antes era uma string, alterar para algo como `{ text: 'blabla', images: ['/static/foo.png'], files: ['/static/bar.zip'] }` pode ajudar no próximo passo.
  - Utilizar o array de links para gerar previews dos arquivos enviados (caso sejam imagens, mostrar uma `<img>` pequena, caso contrário algum ícone ou placeholder de sua escolha).

## Como entregar

Crie um repositório no Github. O repositório deve ser privado enquanto não te avaliamos, mas depois da avaliação pode deixar público e utilizar para portfólio se quiser!

Dê permissão de acesso para [@kvdos-argonaut](https://github.com/kvdos-argonaut) ao seu repositório.

É **obrigatório** ter um **README** com todas as instruções para rodar o seu desafio (podem ser comandos `python` e `npm`/`yarn` pra rodar o back e o front separadamente, comandos `docker` ou `docker-compose` se você containerizou o app ou até mesmo um link para o heroku/aws/host de sua preferência com o app rodando).

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
