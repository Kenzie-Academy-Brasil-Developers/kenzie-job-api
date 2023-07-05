<h1 align="center">
  <img alt="KenzieHub" title="KenzieHub" src="https://kenzie.com.br/_next/image?url=%2Fimages%2Flogo.png&w=640&q=75" width="100px" />
</h1>

<h1 align="center">
  KenzieJob - API
</h1>

<p align="center">
  <a href="#endpoints">Endpoints</a>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
</p>

A API tem um total de 13 endpoints, sendo em volta principalmente do usuário (dev) - podendo cadastrar seu perfil, tecnologias que estuda e trabalhos realizados. <br/>

A url base da API é https://kenzie-job-api.onrender.com/

## Rotas que não precisam de autenticação

<h2 align ='center'> Listagem de jobs com o nome da empresa </h2>

Nessa aplicação o usuário sem fazer login ou se cadastrar pode ver os produtos já cadastrados na plataforma, na API podemos acessar a lista dessa forma:

`GET /jobs?_expand=user - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "userId": 1,
    "id": 1,
    "position": "Desenvolvedor FullStack Jr",
    "sallary": 3400,
    "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam quis orci nec felis varius pretium. Nam eu diam erat. Sed libero ante, finibus id nunc suscipit, sagittis sagittis sem. Nam accumsan, turpis sed consequat tincidunt, nibh odio tincidunt nunc, aliquet sodales sem tortor sed lectus.",
    "user": {
      "email": "kenzinho@mail.com",
      "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
      "name": "Kenzinho",
      "age": 38,
      "id": 1
    }
  }
]
```

<h2 align ='center'> Listagem de jobs com filtros </h2>

Nessa aplicação o usuário sem fazer login ou se cadastrar pode ver os produtos já cadastrados na plataforma, na API podemos acessar a lista dessa forma:

`GET /jobs?position_like=dev - FORMATO DA RESPOSTA - STATUS 200`
ou
`GET /jobs?description_like=dev - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "userId": 1,
    "id": 1,
    "position": "Desenvolvedor FullStack Jr",
    "sallary": 3400,
    "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam quis orci nec felis varius pretium. Nam eu diam erat. Sed libero ante, finibus id nunc suscipit, sagittis sagittis sem. Nam accumsan, turpis sed consequat tincidunt, nibh odio tincidunt nunc, aliquet sodales sem tortor sed lectus."
  }
]
```



<h2 align ='center'> Inscrever em uma vaga </h2>

`POST /applications - FORMATO DA REQUISIÇÃO`

```json
{
  "jobId": 1,
  "userId": 1,
  "name": "Tsunode",
  "email": "tsunode@mail.com",
  "linkedin": "https://www.linkedin.com/in/tsunode"
}
```


<h2 align ='center'> Criação da empresa </h2>

`POST /users - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "johndoe@email.com",
  "password": "123456",
  "name": "John Doe",
}
```

Caso dê tudo certo, a resposta será assim:

`POST /users - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvaG5kb2VAZW1haWwuY29tIiwiaWF0IjoxNjg3ODA4MTYzLCJleHAiOjE2ODc4MTE3NjMsInN1YiI6IjMifQ.nWj1gqD4t3x00UTQvfFiK-PQjcgSpzbGeHknpncgC9E",
  "user": {
    "email": "johndoe@email.com",
    "name": "John Doe",
    "id": 3
  }
}
```


<h2 align = "center"> Login como empresa</h2>

`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "johndoe@email.com",
  "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvaG5kb2VAZW1haWwuY29tIiwiaWF0IjoxNjg3ODA4MTYzLCJleHAiOjE2ODc4MTE3NjMsInN1YiI6IjMifQ.nWj1gqD4t3x00UTQvfFiK-PQjcgSpzbGeHknpncgC9E",
  "user": {
    "email": "johndoe@email.com",
    "name": "John Doe",
    "id": 3
  }
}
```

<h2 align ='center'>Consultar usuários</h2>

`GET /users/ - FORMATO DA REQUISIÇÃO`

```json
[
  {
    "email": "kenzinho@mail.com",
    "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
    "name": "Kenzinho",
    "age": 38,
    "id": 1
  }
]
```

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Cadastrar vaga </h2>

`POST /jobs/ - FORMATO DA REQUISIÇÃO`

```json
{
  "position": "Desenvolvedor FullStack Jr",
  "sallary": 3400,
  "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam quis orci nec felis varius pretium. Nam eu diam erat. Sed libero ante, finibus id nunc suscipit, sagittis sagittis sem. Nam accumsan, turpis sed consequat tincidunt, nibh odio tincidunt nunc, aliquet sodales sem tortor sed lectus."
}
```


<h2 align ='center'> Atualizar vaga </h2>

`PUT /jobs/:id - FORMATO DA REQUISIÇÃO`

```json
{
  "position": "Desenvolvedor FullStack Jr",
  "sallary": 3400,
  "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam quis orci nec felis varius pretium. Nam eu diam erat. Sed libero ante, finibus id nunc suscipit, sagittis sagittis sem. Nam accumsan, turpis sed consequat tincidunt, nibh odio tincidunt nunc, aliquet sodales sem tortor sed lectus."
}
```

Também é possível deletar uma vaga, utilizando este endpoint:

`DELETE /jobs/:id`

```
Não é necessário um corpo da requisição.
```

<h2 align ='center'> Listar vagas por empresa </h2>

`GET users/:idCompany/jobs - FORMATO DA REQUISIÇÃO`

```json
[
  {
    "id": 1,
    "position": "Desenvolvedor FullStack Jr",
    "sallary": 3400,
    "description": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nam quis orci nec felis varius pretium. Nam eu diam erat. Sed libero ante, finibus id nunc suscipit, sagittis sagittis sem. Nam accumsan, turpis sed consequat tincidunt, nibh odio tincidunt nunc, aliquet sodales sem tortor sed lectus."
  }
]
```


<h2 align ='center'> Listar candidaturas por empresa </h2>

`GET /jobs/1/applications - FORMATO DA REQUISIÇÃO`

```json
[
  {
    "id": 1,
    "jobId": 1,
    "name": "Tsunode",
    "email": "tsunode@mail.com",
    "linkedin": "https://www.linkedin.com/in/tsunode"
  }
]
```
