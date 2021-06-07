# Code Challenge Yungas Full Stack

O objetivo deste desafio é avaliar a sua maneira de pensar e resolver os problemas propostos.

A forma como você resolverá este desafio é importante para entendermos seus padrões de qualidade, organização, performance, etc. Além dos requisitos que serão citados, diversos outros serão também avaliados (mas esses são surpresa, ok?)

No final, lhe daremos retorno sobre os pontos que achamos positivos e negativos.

A Yungas usa um stack de transição com back-end em Flask e:
- front-end em Jinja+jQuery nos módulos mais antigos;
- front-end Svelte nos módulos mais novos. 

Familiaridade com Svelte não é um requerimento, mas um diferencial. Se você teve experiência com Vue ou React, Svelte será moleza pra você.

Para este desafio, recomendamos que utilize para o back-end Flask, FastAPI, Sanic ou Quartz.

No front-end, utilize Svelte, React+Redux ou Vue. 

*Evite usar Django* (é um ótimo framework, mas tem pouco a ver com a nossa base de código).

*Evite usar Angular ou outro framework* (Svelte é o que você vai lidar no dia-a-dia, React+Redux e Vue são razoavelmente similares).

Preferimos *fortemente* que evite utilizar componentes prontos - afinal, queremos ver o seu código e a sua maneira de resolver problemas.

Nice-to-have (não é "tudo ou nada", faça o que conseguir!):
- Containerização.
- Testes unitários.
- Testes de integração.
- Declarativo sobre imperativo.
- Composition over inheritance.
- Comentários (pode ser no README) sobre como faria deploy deste app. Como lidaria com:
  - Configs?
  - Secrets?
  - Logs?
  - Quanto mais detalhes, melhor!
- Deploy deste app na AWS ou Heroku (mas não precisa gastar dinheiro!).

Must-have:
- Projeto organizado.
- Código limpo.
- Front-end com componentes simples e reutilizáveis.
- Back-end com estrutura clara e responsabilidades bem definidas.

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
  - Emitir eventos para todos os usuários da sala (fazer um broadcast) quando usuários entrarem na sala.
  - Fazer um broadcast quando receber mensagens de usuários da sala.
  - Fazer um broadcast quando um usuário da sala estiver digitando.
  - Fazer um broadcast quando um usuário da sala que estava digitando parar de digitar.
  - Fazer um broadcast quando um usuário da sala sair da sala.
- Front-end:
  - Pedir ao usuário um username para que ele possa entrar na sala.
  - Emitir ao back-end um evento `connected` quando entrar na sala.
  - Emitir ao back-end um evento `disconnected` quando sair da sala.
  - Emitir ao back-end um evento `message` ao enviar uma mensagem (pode ser via clique em um botão escrito `Enviar`, por exemplo).
  - Quando receber um evento `connected` do back-end, mostrar ou atualizar uma lista de usuários ativos na sala.
  - Quando receber um evento `disconnected` do back-end, atualizar a lista de usuários ativos na sala.
  - Quando receber um evento `message`, mostrar no chat a mensagem recebida (diferenciar mensagens próprias de uma mensagem de outro usuário).


### Requerimentos intermediários
- Back-end:
  - Definir mais salas (Sala 2 e Sala 3, por exemplo).
  - Usuários só podem estar em uma sala por vez.
  - Usuários que estão em uma sala não podem ver mensagens de outras salas.
  - Emitir ao back-end um evento `typing` quando começar a digitar uma mensagem.
  - Emitir ao back-end um evento `stop-typing` quando parar de digitar.
- Front-end:
  - Implementar alguma maneira de trocar de salas (pode ser em abas ou menus laterais).
  - Implementar interface para login ou registro do usuário (antes de entrar em uma sala).
  - Mensagens das salas *não devem aparecer* para usuários não-autenticados.
  - Mostre as informações extras do usuário (nome e email) em algum lugar da tela (um modal que abre ao clicar no usuário na lista, por exemplo).
  - Quando receber um evento `typing`, mostrar em algum lugar na tela qual usuário está digitando (algo como `João is typing...`).
  - Quando receber um evento `stop-typing`, parar de mostrar que aquele usuário está digitando (se João parar de digitar, mas Pedro continua digitando, mostrar `Pedro is typing...`).

### Requerimentos avançados
- Back-end:
  - Faça com que o usuário se registre ou faça login para entrar em uma sala.
  - A autenticação pode ser implementada da maneira que preferir (JWT, Basic Auth, etc). Procure usar uma library popular para o framework que escolheu.
  - `nome`, `username`, `senha` (encriptada, claro) e `email` devem ser persistidos em um banco de dados SQLite.
  - Implementar sessões, de tal maneira que o usuário não precise refazer o login quando der um refresh ou fechar e abrir a aba.
  - A implementação das sessões, assim como da autenticação, fica a seu critério (pode usar uma library que faça ambos).
  - Implementar uma rota HTTP POST `/upload`, que deve:
    - Receber arquivos via FormData (o texto da mensagem ainda deve ir via socket, mas deve esperar o envio dos arquivos).
    - Salvar os arquivos em uma pasta local `/tmp`.
    - Retornar links para esses arquivos (o backend deve servir esses arquivos em `/static/<NOME-DO-ARQUIVO>`).
    - Obs.: No caso de mais de um arquivo, lembre de retornar um array de links.
- Front-end:
  - Ajustar a interface para permitir que arquivos sejam enviados (pode ser um botão `Anexar` ao lado de `Enviar`, por exemplo).
  - Enviar os arquivos via POST para `/upload` (não envie o texto da mensagem!).
  - Uma vez que os arquivos sejam enviados, envie junto do texto da mensagem o array de links que recebeu na response.
    - Obs.: Se a mensagem antes era uma string, alterar para algo como `{ text: 'blabla', images: ['/static/foo.png'], files: ['/static/bar.zip'] }` pode ajudar no próximo passo.
  - Utilizar o array de links para gerar previews dos arquivos enviados (caso sejam imagens, mostrar uma `<img>` pequena, caso contrário algum ícone ou placeholder de sua escolha).

## Como entregar

Crie um repositório no Github. O repositório deve ser privado enquanto não te avaliamos, mas depois da avaliação pode deixar público e utilizar para portfólio se quiser!

Dê permissão de acesso para [@kvdos-argonaut](https://github.com/kvdos-argonaut) ao seu repositório.

É obrigatório ter um **README** com todas as instruções sobre o seu desafio.

Assim que finalizar, envie um link para o repositório para o e-mail `marcos@yungas.com.br`, para que possamos avaliar.

## Boa sorte!
