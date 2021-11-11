# <span>📝</span> task-gamefication-api

Esse repositório compreende a API task-gamefication-api, que tem como objetivo auxiliar o usuário que está começando a jornada de morar sozinho. Neste caso ajudando na organização de suas tarefas e contando com um comunidade para realizar seus questionamentos.

## Endpoints

A API possuí <b>27 endpoints</b>, que são divididos em 5 categorias:

<ul>
<h3><b>Users Requests</b></h3>
<p>Esta pasta guarda todos os endpoints relacionados ao usuário. Desta forma é possível: </p>
<li>Realizar o cadastro do usuário, caso o mesmo ainda não o tenha</li>
<li>Logar na aplicação, caso o mesmo já seja cadastrado</li>
<li>Exibir as perguntas que o usuário realizou</li>
<li>Exibir o histórico de comentários que ele fez nas perguntas da comunidade</li>
<li>Exibir o nível atual do usuário</li>
<li>Exibir as conquistas do usuário</li>
<li>Atualizar os pontos de XP do usuário</li>
</ul>

</br>

<ul>
<h3><b>Tasks Requests</b></h3>
<p>Esta pasta guarda todos os endpoints relacionados as tarefas do usuário. Desta forma é possível: </p>

<li>Exibir todas as tarefas cadastradas do usuário</li>
<li>Adicionar nova tarefa</li>
<li>Deletar  tarefa</li>
<li>Editar tarefa</li>
</ul>
</br>

<ul>
<h3><b>Community Requests</b></h3>
<p>Esta pasta guarda todos os endpoints relacionados as perguntas que o usuário faz no comunidade e a interação de comentários. Desta forma ele é dividido em 2 subpastas <b>Comments e Quests</b>. </p>
 
<h4><b>Quests</b></h4>
<li>Exibir todas as perguntas</li>
<li>Adicionar nova pergunta</li>
<li>Deletar  pergunta</li>
<li>Editar pergunta</li>
<br>
<h4><b>Comments</b></h4>
<li>Exibir todos as comentários</li>
<li>Exibir os comentários de uma pergunta específica</li>
<li>Adicionar novo comentário</li>
<li>Deletar  comentário</li>
<li>Editar comentário</li>

</ul>
</br>
<ul>
<h3><b>Levels Requests</b></h3>
<p>Esta pasta guarda todos os endpoints relacionados ao Level, desta forma é possível:</p>
<li>Consultar a biblioteca de níveis</li>
<li>Verificar os níveis de todos os usuários</li>
<li>Atualizar o nível de um usuário</li>
<li>Adicionar o primeiro nível para o usuário</li>
</ul>
</br>
<ul>
<h3><b>Badges Requests</b></h3>
<p>Esta pasta guarda todos os endpoints relacionados as Badges, desta forma é possível:</p>
<li>Adicionar badges no perfil do usuário</li>
<li>Verificar as badges de todos os usuários</li>
<li>Consultar biblioteca de badges</li>
</ul>
<br>

**baseUrl**: https://tasks-gamefication-api.herokuapp.com

## 👤 User

</br>

### <span>&#10162;</span> Login

POST /login <br/>

Este endpoint é reservado para realizar o login do usuário previamente cadastrado. Ele retorna o accessToken que será utilizado nos próximos endpoints.

`POST /login - FORMATO DE ENTRADA:`

```json
[
  {
    "email": "madu@mail.com",
    "password": "123456"
  }
]
```

`POST /login - FORMATO DE SAÍDA - 200`

```json
[
  {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hZHVAbWFpbC5jb20iLCJpYXQiOjE2MzY1OTY2MzksImV4cCI6MTYzNjYwMDIzOSwic3ViIjoiMSJ9.wjwMrYOlDp6cUa7CiFaBt_7ZM9d-bxJt_Fk9-i5fMLc",
    "user": {
      "email": "madu@mail.com",
      "firstName": "madu",
      "lastName": "Rubini",
      "xp": 0,
      "id": 1
    }
  }
]
```

### <span>&#10162;</span> Cadastro

POST /register <br/>

Este endpoint é para cadastrar os usuários que ainda não estão previamente cadastrados. Neste caso o retorno já possuí o accessToken para a aplicação.

`POST /register - FORMATO DE ENTRADA:`

```json
[
  {
    "firstName": "duda",
    "lastName": "Santos",
    "email": "duda@mail.com",
    "password": "123456",
    "xp": 0
  }
]
```

`POST /register - FORMATO DE SAÍDA - 200`

```json
[
  {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImR1ZGFAbWFpbC5jb20iLCJpYXQiOjE2MzY1OTkzMDEsImV4cCI6MTYzNjYwMjkwMSwic3ViIjoiMyJ9.02pHBrMjBIg0ga4K65cg4BZZXUWXYRK4ylpnV6AK-ao",
    "user": {
      "email": "duda@mail.com",
      "firstName": "duda",
      "lastName": "Santos",
      "xp": 0,
      "id": 3
    }
  }
]
```

### <span>❓</span> User Quests

Este endpoint é para exibir as perguntas do usuário cadastrado. Neste caso na url da requisição passamos o userId da pessoa logada.
<br>Necessita de autenticação: **Bearer: token**

`GET /users/{userId}/quests - FORMATO DE SAÍDA:`

```json
[
  {
    "body": "Como tirar a gordura do box do banheiro?",
    "likes": 0,
    "userId": 1,
    "id": 2
  }
]
```

### <span>💬</span> User Comments

Este endpoint é para exibir os comentários do usuário cadastrado. Neste caso na url da requisição passamos o userId da pessoa logada e o questId da pergunta escolhida.
<br>Necessita de autenticação: **Bearer: token**

`GET /users/{userId}/comments - FORMATO DE SAÍDA:`

```json
[
  {
    "comment": "O ideal é ter um desengordurante de cozinha em mãos para essa operação",
    "questId": 2,
    "userId": 1,
    "id": 1
  }
]
```

### **Get User Level**

Este endpoint é para exibir o nível do usuário cadastrado. Neste caso no corpo da requisição passamos o userId da pessoa logada.
<br>Necessita de autenticação: **Bearer: token**

`GET /users/{userId}/allLevels - FORMATO DE SAÍDA:`

```json
[
  {
    "title": "Bronze",
    "reqXp": 30,
    "level": 2,
    "LevelId": 3,
    "status": false,
    "userId": 1,
    "id": 1
  }
]
```

### **Udpate user XP**

Este endpoint é para atualizar o XP do usuário conforme ele conclua uma tarefa.
Na URL passamos o usuário que queremos atualizar a pontuação e no corpo da requisição o parâmetro que queremos atualizar.
<br>Necessita de autenticação: **Bearer: token**

`PATCH /users/{userId}- FORMATO DE ENTRADA:`

```json
[
  {
    "xp": 30
  }
]
```

`PATCH /users/{userId} - FORMATO DE SAÍDA:`

```json
[
  {
    "email": "madu@mail.com",
    "password": "$2a$10$eJyGYZ0aedKPnF8MUp8ttu7IkFyyElopV53L9Qnnlq4i0j8pOnEkS",
    "firstName": "madu",
    "lastName": "Rubini",
    "xp": 30,
    "id": 1
  }
]
```

### **Get User Badges**

Este endpoint é para exibir as conquistas do usuário cadastrado. Neste caso no corpo da requisição passamos o userId da pessoa logada.
<br>Necessita de autenticação: **Bearer: token**

`GET /users/{userId}/allBadges - FORMATO DE SAÍDA:`

```json
[
  {
    "title": "Novo no pedaço",
    "img": "https://picsum.photos/200",
    "description": "Você fez seu primeiro login!",
    "BadgeId": 1,
    "status": true,
    "userId": 1,
    "id": 1
  },
  {
    "title": "Questionad@r",
    "img": "https://picsum.photos/200",
    "description": "Você fez sua primeira pergunta na comunidade!",
    "BadgeId": 2,
    "status": true,
    "userId": 1,
    "id": 2
  }
]
```

</br>

## <span>📝</span> Tasks

Este endpoint é para acessar as tarefas que o usuário já tem cadastrado. Passando como parâmetro o userId da pessoa logada.<br/>
Necessita de autenticação: **Bearer: token**

`GET /tasks?userId={userId} - FORMATO DE SAÍDA - STATUS 200:`<br/>

```json
[
  {
    "title": "Lavar a Louça",
    "difficulty": "Easy",
    "description": "Lavar todos os pratos e talheres",
    "xp": 0,
    "finished": false,
    "userId": 1,
    "id": 1
  }
]
```

#### ➕ **Add a new Task**

No corpo da requisição é necessário passar o userId do usuário logado.
Necessita de autenticação: **Bearer: token**

`POST /tasks - FORMATO DE ENTRADA:`

```json
[
  {
    "title": "Lavar o banheiro",
    "difficulty": "Medium",
    "xp": 0,
    "finished": false,
    "userId": 1
  }
]
```

`POST /tasks - FORMATO DE SAÍDA - 200`

```json
[
  {
    "title": "Lavar o banheiro",
    "difficulty": "Medium",
    "xp": 0,
    "finished": false,
    "userId": 1,
    "id": 3
  }
]
```

#### <span> ❌</span> **Delete a Task**

Para deletar uma tarefa é necessário passar o Id da task como parâmetro na URL.
Necessita de autenticação: **Bearer: token**

`DELETE /tasks/{taskId} - FORMATO DE SAÍDA - 200`

```json
[{}]
```

#### <span>&#9999;</span> **Edit a Task**

Para editar uma tarefa é necessário passar o Id da task como parâmetro na URL e desta forma alterar os campos desejados.
Necessita de autenticação: **Bearer: token**

`PATCH /tasks/{taskId} - FORMATO DE ENTRADA:`

```json
[
  {
    "title": "Trocar a resistência do chuveiro",
    "difficulty": "Hard",
    "finished": true
  }
]
```

`PATCH /tasks/{taskId} - FORMATO DE SAÍDA - 200`

```json
[
  {
    "title": "Trocar a resistência do chuveiro",
    "difficulty": "Hard",
    "xp": 0,
    "finished": true,
    "userId": 1,
    "id": 3
  }
]
```

</br>

## <span>👥</span> comunidade

### ? Quests

Esta rota é livre para todos os usuários visualizarem, porém apenas os usuários logados podem interagir na aplicação, como comentar e perguntar no comunidade.

`GET /quests/ - FORMATO DE SAÍDA - 200`

```json
[
  {
    "body": "Como saber o dia de amanhã?",
    "likes": 2,
    "userId": 1,
    "id": 2
  },
  {
    "body": "Como tirar mancha de vinho do tapete?",
    "likes": 0,
    "userId": 2,
    "id": 3
  }
]
```

### ➕ Add a new Quest

Para adicionar uma nova pergunta, é necessário passar no corpo da requisição o userId do usuário logado e a pergunta feita. Likes sempre será 0 por default.
Necessita de autenticação: **Bearer: token**

`POST /quests/ - FORMATO DE ENTRADA - 200`

```json
[
  {
    "body": "Como saber se minha tomada é 110? ou 220?",
    "likes": 0,
    "userId": 1
  }
]
```

`POST /quests/ - FORMATO DE SAÍDA - 200`

```json
[
  {
    "body": "Como saber se minha tomada é 110? ou 220?",
    "likes": 0,
    "userId": 1,
    "id": 2
  }
]
```

### &#9999; Edit a Quest

Para editar uma pergunta, é necessário passar no parâmetro da URL a questId da pergunta na qual o usuário deseja editar.
Necessita de autenticação: **Bearer: token**

`PATCH /quests/{questId} - FORMATO DE ENTRADA - 200`

```json
[
  {
    "body": "Como armazenar os vegetais na geladeira?",
    "likes": 0
  }
]
```

`PATCH /quests/{questId} - FORMATO DE SAÍDA - 200`

```json
[
  {
    "body": "Como armazenar os vegetais na geladeira?",
    "likes": 2
  }
]
```

### ❌ Remove a Quest

Para remover uma pergunta, é necessário passar no parâmetro da URL a questId da pergunta na qual o usuário deseja remover.
Necessita de autenticação: **Bearer: token**

`DELETE /quests/{questId} - FORMATO DE SAÍDA - 200`

```json
[{}]
```

<br>

### 💬 Comments

Esta rota é livre para todos os usuários visualizarem, porém apenas os usuários logados podem interagir na aplicação, como comentar e editar os comentários.

`GET /comments - FORMATO DE SAÍDA - 200`

```json
[
  {
    "comment": "O ideal é ter um multimetro em mãos para essa operação",
    "questId": 2,
    "userId": 1,
    "id": 1
  },
  {
    "comment": "Vale a pena verificar a voltagem da sua casa",
    "questId": 2,
    "userId": 2,
    "id": 2
  },
  {
    "comment": "Coloca mais água para ferver, desta forma ele não grudará",
    "questId": 3,
    "userId": 1,
    "id": 3
  }
]
```

### 💬 Get Specific Comments of a quest

`GET /quests/{questId}/comments- FORMATO DE SAÍDA - 200`

```json
[
  {
    "comment": "O ideal é ter um multimetro em mãos para essa operação",
    "questId": 2,
    "userId": 1,
    "id": 1
  }
]
```

### ➕ Add a new Comment

Para adicionar uma nova pergunta, é necessário passar no corpo da requisição o userId do usuário logado e o questId da pergunta na qual o usuário deseja comentar.
Necessita de autenticação: **Bearer: token**

`POST /comments - FORMATO DE ENTRADA - 200`

```json
[
  {
    "comment": "O ideal é ter um multimetro em mãos para essa operação",
    "questId": 2,
    "userId": 1
  }
]
```

`POST /comments - FORMATO DE SAÍDA - 200`

```json
[
  {
    "comment": "O ideal é ter um multimetro em mãos para essa operação",
    "questId": 2,
    "userId": 1,
    "id": 1
  }
]
```

### &#9999; Edit a Comment

Para editar um comentário, é necessário passar no parâmetro da URL o id do comentário na qual o usuário deseja editar.
Necessita de autenticação: **Bearer: token**

`PATCH /comments/{commentId} - FORMATO DE ENTRADA - 200`

```json
[
  {
    "comment": "Não precisa fazer esse processo, é possível lavar apenas com água e sabão"
  }
]
```

`PATCH /comments/{commentId} - FORMATO DE SAÍDA - 200`

```json
[
  {
    "comment": "Não precisa fazer esse processo, é possível lavar apenas com água e sabão",
    "questId": 1,
    "id": 1
  }
]
```

### ❌ Delete a Comment

Para deletar um comentário, é necessário passar no parâmetro da URL o id do comentário na qual o usuário deseja deletar.
Necessita de autenticação: **Bearer: token**

`DELETE /comments/{commentId} - FORMATO DE SAÍDA - 200`

```json
[{}]
```

<br>

## Levels

<br>

### Get Levels Lib

Para consultar a biblioteca de níveis é necessário apenas estar logado na aplicação.
Necessita de autenticação: **Bearer: token**

`GET /levels - FORMATO DE SAÍDA - 200`

```json
[
  {
    "title": "Noob",
    "reqXp": 0,
    "level": 0,
    "LevelId": 1,
    "status": false
  },
  {
    "title": "Ferro",
    "reqXp": 10,
    "level": 1,
    "LevelId": 2,
    "status": false
  },
  {
    "title": "Bronze",
    "reqXp": 30,
    "level": 2,
    "LevelId": 3,
    "status": false
  }
]...
```

### Get AllLevels Activity

Este endpoint é reservado para exibir os níveis de todos os usuários da aplicação.
Necessita de autenticação: **Bearer: token**

`GET /allLevels - FORMATO DE SAÍDA - 200`

```json
[
  {
    "title": "Bronze",
    "reqXp": 30,
    "level": 2,
    "LevelId": 3,
    "status": false,
    "userId": 1,
    "id": 1
  }
]
```

### Add a level to User

Este endpoint é reservado para adicionar um nível para o usuário cadastrado. Desta forma vamos passar no corpo da requisição o objeto referente o nível à ser adicionado, passando também o userId do usuário desejado.<br>
Necessita de autenticação: **Bearer: token**

`POST /allLevels - FORMATO DE ENTRADA - 200`

```json
[
  {
    "title": "Noob",
    "reqXp": 0,
    "level": 0,
    "LevelId": 1,
    "status": false,
    "userId": 1
  }
]
```

`POST /allLevels - FORMATO DE SAÍDA - 200`

```json
[
  {
    "title": "Noob",
    "reqXp": 0,
    "level": 0,
    "LevelId": 1,
    "status": false,
    "userId": 1,
    "id": 1
  }
]
```

### Update a level

Este endpoint é reservado para atualizar um nível para o usuário conforme sua evolução nos pontos de XP. Desta forma vamos passar no corpo da requisição o objeto referente o nível à ser atualizado. Passando como parametro na URL o id do nível a ser atualizado<br>
Necessita de autenticação: **Bearer: token**

`PATCH /allLevels/{userLevelId} - FORMATO DE ENTRADA - 200`

```json
[
  {
    "title": "Bronze",
    "reqXp": 30,
    "level": 2,
    "LevelId": 3,
    "status": false
  }
]
```

`PATCH /allLevels/{userLevelId} - FORMATO DE SAÍDA - 200`

```json
[
  {
    "title": "Bronze",
    "reqXp": 30,
    "level": 2,
    "LevelId": 3,
    "status": false,
    "userId": 1,
    "id": 1
  }
]
```

<br>

## Badges

<br>

### Get Badges Lib

Para consultar a biblioteca de conquistas é necessário apenas estar logado na aplicação.
Necessita de autenticação: **Bearer: token**

`GET /badges - FORMATO DE SAÍDA - 200`

```json
[
 {
    "title": "Novo no pedaço",
    "img": "https://picsum.photos/200",
    "description": "Você fez seu primeiro login!",
    "BadgeId": 1,
    "status": false
  },
  {
    "title": "Questionad@r",
    "img": "https://picsum.photos/200",
    "description": "Você fez sua primeira pergunta na comunidade!",
    "BadgeId": 2,
    "status": false
  },
  {
    "title": "Parceir@",
    "img": "https://picsum.photos/200",
    "description": "Você fez seu primeiro comentário em uma pergunta!",
    "BadgeId": 3,
    "status": false
  }
]...
```

### Get AllBadges Activity

Este endpoint é reservado para exibir os níveis de todos os usuários da aplicação.
Necessita de autenticação: **Bearer: token**

`GET /allBadges - FORMATO DE SAÍDA - 200`

```json
[
  {
    "title": "Novo no pedaço",
    "img": "https://picsum.photos/200",
    "description": "Você fez seu primeiro login!",
    "BadgeId": 1,
    "status": true,
    "userId": 1,
    "id": 1
  },
  {
    "title": "Questionad@r",
    "img": "https://picsum.photos/200",
    "description": "Você fez sua primeira pergunta na comunidade!",
    "BadgeId": 2,
    "status": true,
    "userId": 1,
    "id": 2
  }
]
```

### Add a level to User

Este endpoint é reservado para adicionar uma conquista para o usuário cadastrado. Desta forma vamos passar no corpo da requisição o objeto referente a conquista à ser adicionada, passando também o userId do usuário desejado.<br>
Necessita de autenticação: **Bearer: token**

`POST /allBadges - FORMATO DE ENTRADA - 200`

```json
[
  {
    "title": "Questionad@r",
    "img": "https://picsum.photos/200",
    "description": "Você fez sua primeira pergunta na comunidade!",
    "BadgeId": 2,
    "status": true,
    "userId": 1
  }
]
```

`POST /allBadges - FORMATO DE SAÍDA - 200`

```json
[
  {
    "title": "Questionad@r",
    "img": "https://picsum.photos/200",
    "description": "Você fez sua primeira pergunta na comunidade!",
    "BadgeId": 2,
    "status": true,
    "userId": 1,
    "id": 2
  }
]
```
