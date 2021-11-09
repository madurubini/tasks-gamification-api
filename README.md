# <span>📝</span> task-gamefication-api

Esse repositório compreende a API task-gamefication-api, que tem como objetivo auxiliar o usuário que está começando a jornada de morar sozinho. Neste caso ajudando na organização de suas tarefas e contando com um fórum para realizar seus questionamentos com a comunidade.

## Endpoints

A API possuí <b>17 endpoints</b>, que são divididos em 3 categorias:

<ul>
<h3><b>Users Requests</b></h3>
<p>Esta pasta guarda todos os endpoints relacionados ao usuário. Desta forma é possível: </p>
<li>Realizar o cadastro do usuário, caso o mesmo ainda não o tenha</li>
<li>Logar na aplicação, caso o mesmo já seja cadastrado</li>
<li>Exibir as perguntas que o usuário realizou</li>
<li>Exibir o histórico de comentários que ele fez nas perguntas do fórum</li>
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
<h3><b>Fórum Requests</b></h3>
<p>Esta pasta guarda todos os endpoints relacionados as perguntas que o usuário faz no fórum e a interação de comentários. Desta forma ele é dividido em 2 subpastas <b>Comments e Quests</b>. </p>
 
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

**baseUrl**: www.esperandofazeropushnoheroku.com

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
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hZHVAbWFpbC5jb20iLCJpYXQiOjE2MzY0Mjk4MzksImV4cCI6MTYzNjQzMzQzOSwic3ViIjoiMSJ9.eKnTns3R4-dYjlVBkaQtKCrMEh2XmXS9tQB9snwwFOQ",
    "user": {
      "email": "madu@mail.com",
      "firstName": "madu",
      "lastName": "Rubini",
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
    "firstName": "Madu",
    "lastName": "Rubini",
    "email": "madu@mail.com",
    "password": "123456"
  }
]
```

`POST /register - FORMATO DE SAÍDA - 200`

```json
[
  {
    "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im1hZHVAbWFpbC5jb20iLCJpYXQiOjE2MzY0MTQyODEsImV4cCI6MTYzNjQxNzg4MSwic3ViIjoiMSJ9.TbIQO0V8NbGDw_HNx1VE-1xDes_M39Q-iedV4P6DdHY",
    "user": {
      "email": "madu@mail.com",
      "firstName": "madu",
      "lastName": "Rubini",
      "id": 1
    }
  }
]
```

### <span>❓</span> User Quests

Este endpoint é para exibir as perguntas do usuário cadastrado. Neste caso no corpo da requisição passamos o userId da pessoa logada.
<br>Necessita de autenticação: **Bearer: token**

`GET /users/{questId}/quests - FORMATO DE SAÍDA:`

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

Este endpoint é para exibir os comentários do usuário cadastrado. Neste caso no corpo da requisição passamos o userId da pessoa logada e o questId da pergunta escolhida.
<br>Necessita de autenticação: **Bearer: token**

`GET /users/{questId}/comments - FORMATO DE SAÍDA:`

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

## <span>👥</span> Fórum

### ? Quests

Esta rota é livre para todos os usuários visualizarem, porém apenas os usuários logados podem interagir na aplicação, como comentar e perguntar no fórum.

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

`POST /quests/ - FORMATO DE SAÍDA - 200`

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
