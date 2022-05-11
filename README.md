# **Adopet API**

## **Base Url**: https://adopet-api-cm3.herokuapp.com

---

## **Users**

### <br>**Registrar usuário:**

method: POST

endpoint: /register

body:

```
{
	"email": "teste@gmail.com",
	"password": "strongestPassword",
	"name": "João",
	"phone": "22998001100",
	"avatar": "link_img",
	"type":"institution"
}
```

<br>**Exemplo de respostas:**

cadastrado com sucesso:<br>

```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlQGdtYWlsLmNvbSIsImlhdCI6MTY1MjMwNDcwNywiZXhwIjoxNjUyMzA4MzA3LCJzdWIiOiIyIn0.5m_y34NmofYKTwfWn0J3rP0Y10rXYBfGCDffXr3moNw",
	"user": {
		"email": "teste@gmail.com",
		"name": "João",
		"phone": "22998001100",
		"avatar": "link_img",
		"type": "institution",
		"id": 1
	}
}
```

se o email já tiver cadastrado:<br>

```
"Email already exists"
```

---

### **Logar usuário:**

method: POST

endpoint: /login

body:

```
{
  "email": "teste@gmail.com",
  "password": "strongestPassword"
}
```

<br>**Exemplo de respostas:**

logado com sucesso:<br>

```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlQGdtYWlsLmNvbSIsImlhdCI6MTY1MjMwNDc4MiwiZXhwIjoxNjUyMzA4MzgyLCJzdWIiOiIyIn0.EGU1MJD-TVt-Sitr3wdE-qFIXmcLa6Kn6jqCWu0zKCU",
	"user": {
		"email": "teste@gmail.com",
		"name": "João",
		"phone": "22998001100",
		"avatar": "link_img",
		"type": "institution",
		"id": 1
	}
}
```

email não cadastrado:

```
"Cannot find user"
```

senha incorreta:

```
"Incorrect password"
```

---

### **Listar todos os usuários:**

method: GET

endpoint: /644/users

body: empty

<br>**Exemplo de respostas:**

```
[
	{
		"email": "teste@gmail.com",
		"password": "$2a$10$Rk9usS3xbwLo8PZyhSEoKukkHLyLK7XxIv3IdZyAiPgvNeveN9DiG",
		"name": "João",
		"phone": "22998001100",
		"avatar": "link_img",
		"type": "institution",
		"id": 1
	}
]
```

---

### **Listar usuários by id**:

method: GET

endpoint: /644/users/:id

body: empty

<br>**Exemplo de respostas:**

se o id existe:

```
//.../644/users/1

{
	"email": "teste@gmail.com",
	"password": "$2a$10$Rk9usS3xbwLo8PZyhSEoKukkHLyLK7XxIv3IdZyAiPgvNeveN9DiG",
	"name": "João",
	"phone": "22998001100",
	"avatar": "link_img",
	"type": "institution",
	"id": 1
}
```

se o id não existe:

```
{}
```

---

### **Listar usuários por tipo:**

method: GET

endpoint: /644/users?type=:tipo

body: empty

tipos possíveis: institution, person

<br>**Exemplo de respostas:**

se existe algum objeto com o tipo:<br>

```
//type=institution

[
	{
		"email": "teste@gmail.com",
		"password": "$2a$10$Rk9usS3xbwLo8PZyhSEoKukkHLyLK7XxIv3IdZyAiPgvNeveN9DiG",
		"name": "João",
		"phone": "22998001100",
		"avatar": "link_img",
		"type": "institution",
		"id": 1
	}
]
```

se não existe um objeto com o tipo:<br>

```
[]
```

---

### **Editar usuário pelo id:**

method: PATCH

endpoint: /644/users/:id

authentication (bearer): token do usuário

body:

```
//propriedade a ser modificada

{
	"name": "João Patcheado"
}
```

<br>**Exemplo de respostas:**

se a propriedade existe no objeto:

```
{
	"email": "teste@gmail.com",
	"password": "$2a$10$Rk9usS3xbwLo8PZyhSEoKukkHLyLK7XxIv3IdZyAiPgvNeveN9DiG",
	"name": "João Patcheado",
	"phone": "22998001100",
	"avatar": "link_img",
	"type": "institution",
	"id": 1
}
```

**Nota:** se a propriedade não existir, será criada uma nova propriedade com o nome e valor que foram enviados.

---

## **Animals**

### <br>**Cadastrar um animal:**

method: POST

endpoint: /644/animals

authentication (bearer): token do usuário pertencente ao userId

body:

```
{
	"userId": 1,
	"species": "cat",
	"sex": "m",
	"img":"img_link",
	"size": "pequeno",
	"more_info":""
}
```

<br>**Exemplo de respostas:**

se userId foi informado corretamente:

```
{
	"userId": 1,
	"species": "cat",
	"sex": "m",
	"img":"img_link",
	"size": "pequeno",
	"more_info":"",
	"id": 1
}
```

se o userId informado for diferente do id do usuário que detem o token fornecido:

```
"Private resource creation: request body must have a reference to the owner id"
```

---

### **Listar todos os animais:**

method: GET

endpoint: /644/animals

body: empty

<br>**Exemplo de respostas:**

```
[
	{
		"userId": 1,
		"species": "cat",
		"sex": "m",
		"img":"img_link",
		"size": "pequeno",
		"more_info":"",
		"id": 1
	}
]
```

---

### **Listar animal por id:**

method: GET

endpoint: /644/animals/:id

body: empty

<br>**Exemplo de respostas:**

```
// .../644/animals/1

{
	"userId": 1,
	"species": "cat",
	"sex": "m",
	"img":"img_link",
	"size": "pequeno",
	"more_info":"",
	"id": 1
}
```

---

### **Listar animal por espécie:**

method: GET

endpoint: /644/animals?species=:species

espécies possíveis: dog e cat

body: empty

<br>**Exemplo de respostas:**

```
// .../644/animals?species=cat

[
	{
		"userId": 1,
		"species": "cat",
		"sex": "m",
		"img":"img_link",
		"size": "pequeno",
		"more_info":"",
		"id": 1
	}
]
```

---

### **Listar animal por usuário:**

method: GET

endpoint: /644/animals?userId=:id

body: empty

<br>**Exemplo de respostas:**

```
// .../644/animals?userId=1

[
	{
		"userId": 1,
		"species": "cat",
		"sex": "m",
		"img":"img_link",
		"size": "pequeno",
		"more_info":"",
		"id": 1
	}
]
```

---

### **Editar animal pelo id:**

method: PATCH

endpoint: /644/animals/:id

authentication (bearer): token do usuário que cadastrou o animal

body:

```
//propriedade a ser modificada

{
	"img":"outro-link"
}
```

<br>**Exemplo de respostas:**

se a propriedade existe no objeto:

```
{
	"userId": 1,
	"species": "cat",
	"sex": "m",
	"img": "outro-link",
	"size": "",
	"more_info": "",
	"id": 1
}
```

**Nota:** se a propriedade não existir, será criada uma nova propriedade com o nome e valor que foram enviados.

---

### **Deletar animal pelo id:**

method: DELETE

endpoint: /644/animals/:id

authentication (bearer): token do usuário que cadastrou o animal

body: empty

<br>**Exemplo de respostas:**

se o id e token estiverem corretos:

```
{}
```

se o id não existir:

```
"Cannot read properties of undefined (reading 'userId')"
```

se tentar deletar o animal criado por outro usuário:

```
"Private resource access: entity must have a reference to the owner id"
```
