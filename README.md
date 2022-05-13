# **Adopet API**

## **Base Url**: https://adopet-api-cm3.herokuapp.com

---

## **Users**

### <br>**Registrar usuário:**

method: POST

endpoint: /register

body:

se for instituição:

```
{
	"name": "Abrigo do Norte",
	"email": "ong@email.com",
	"password": "12345678",
	"phone": "22998001100",
	"type":"instituicao",
	"cep":"28940000",
	"moreInfo":"A instituição Abrigo do Norte foca em retirar os animais que estão morando nas ruas e prepará-los para receberem um novo lar.",
	"avatar": "link_img"
}
```

se for usuário comum:

```
{
	"email": "joao@email.com",
	"name": "João da Silva",
	"password": "12345678",
	"phone": "22998001100",
	"type":"pessoa",
	"avatar": "link_img"
}
```

<br>**Exemplo de respostas:**

cadastrado com sucesso:<br>

```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im9uZ0BlbWFpbC5jb20iLCJpYXQiOjE2NTI0NTIwMjUsImV4cCI6MTY1MjQ1NTYyNSwic3ViIjoiMiJ9.u5q65gFbs7LABD1ybR7dH74RN3gdZyfk-cW9bQxvNLA",
	"user": {
		"email": "ong@email.com",
		"name": "Abrigo do Norte",
		"phone": "22998001100",
		"type": "instituicao",
		"cep": "28940000",
		"moreInfo": "A instituição Abrigo do Norte foca em retirar os animais que estão morando nas ruas e prepará-los para receberem um novo lar.",
		"avatar": "link_img",
		"id": 2
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
  "email": "joao@email.com",
	"password": "12345678"
}
```

<br>**Exemplo de respostas:**

logado com sucesso:<br>

```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImpvYW9AZW1haWwuY29tIiwiaWF0IjoxNjUyNDU2OTUyLCJleHAiOjE2NTI0NjA1NTIsInN1YiI6IjEifQ.mggrTMya3uB6z-8g1pK96BszCk1R_jdF-x02oX78P04",
	"user": {
		"email": "joao@email.com",
		"name": "João da Silva",
		"phone": "22998001100",
		"type": "pessoa",
		"avatar": "",
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
		"email": "joao@email.com",
		"password": "$2a$10$MU/9zrAw1q0HfHIdpXg1sOXMQRkMerjz5Pe.EEQbEuXu9pSoJLHTO",
		"name": "João da Silva",
		"phone": "22998001100",
		"type": "pessoa",
		"avatar": "",
		"id": 1
	},
	{
		"email": "ong@email.com",
		"password": "$2a$10$HIryiV4gLqyClQDZ3QsrZ.iSWGMkXQoBeVhCBWE2/L7H3i5c3Zg.K",
		"name": "Abrigo do Norte",
		"phone": "22998001100",
		"type": "instituicao",
		"cep": "28940000",
		"moreInfo": "A instituição Abrigo do Norte foca em retirar os animais que estão morando nas ruas e prepará-los para receberem um novo lar.",
		"avatar": "",
		"id": 2
	}
]
```

---

### **Listar usuários by id**:

method: GET

endpoint: /644/users/:id

body: empty

<br>**Exemplo de respostas:**

exemplo de endpoint: /644/users/1

se o id existe:

```
{
	"email": "joao@email.com",
	"password": "$2a$10$MU/9zrAw1q0HfHIdpXg1sOXMQRkMerjz5Pe.EEQbEuXu9pSoJLHTO",
	"name": "João da Silva",
	"phone": "22998001100",
	"type": "pessoa",
	"avatar": "",
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

exemplo de endpoint: /644/users?type=instituicao

se existe algum objeto com o tipo:<br>

```
[
	{
		"email": "ong@email.com",
		"password": "$2a$10$HIryiV4gLqyClQDZ3QsrZ.iSWGMkXQoBeVhCBWE2/L7H3i5c3Zg.K",
		"name": "Abrigo do Norte",
		"phone": "22998001100",
		"type": "instituicao",
		"cep": "28940000",
		"moreInfo": "A instituição Abrigo do Norte foca em retirar os animais que estão morando nas ruas e prepará-los para receberem um novo lar.",
		"avatar": "",
		"id": 2
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
{
	"name": "João da Silva Souza"
}
```

<br>**Exemplo de respostas:**

exemplo de endpoint: .../644/users/1

se a propriedade existe no objeto:

```
{
	"email": "joao@email.com",
	"password": "$2a$10$MU/9zrAw1q0HfHIdpXg1sOXMQRkMerjz5Pe.EEQbEuXu9pSoJLHTO",
	"name": "João da Silva Souza",
	"phone": "22998001100",
	"type": "pessoa",
	"avatar": "",
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
	"userId":2,
	"name": "bolinha",
	"species": "dog",
	"sex":"m",
	"size": "medium",
	"img":"https://uploaddeimagens.com.br/images/003/866/643/original/cao5_1.png",
	"moreInfo":"Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ac nibh ut felis scelerisque finibus sit amet in tortor. Quisque fringilla tempus ex id mollis. Fusce eu nunc placerat, tempor quam sed, lobortis lacus. Donec interdum ipsum eros, nec sollicitudin diam pretium in. Duis sagittis sem vel ante ultricies, laoreet ornare ipsum tincidunt."
}
```

<br>**Exemplo de respostas:**

se userId foi informado corretamente:

```
{
	"userId": 2,
	"name": "bolinha",
	"species": "dog",
	"sex": "m",
	"size": "medium",
	"img": "https://uploaddeimagens.com.br/images/003/866/643/original/cao5_1.png",
	"moreInfo": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ac nibh ut felis scelerisque finibus sit amet in tortor. Quisque fringilla tempus ex id mollis. Fusce eu nunc placerat, tempor quam sed, lobortis lacus. Donec interdum ipsum eros, nec sollicitudin diam pretium in. Duis sagittis sem vel ante ultricies, laoreet ornare ipsum tincidunt.",
	"id": 9
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
		"name": "fiona",
		"species": "dog",
		"sex": "f",
		"size": "small",
		"img": "https://uploaddeimagens.com.br/images/003/866/666/original/cao1_1.png",
		"moreInfo": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ac nibh ut felis scelerisque finibus sit amet in tortor. ",
		"id": 1
	},
	{
		"userId": 1,
		"name": "maxx",
		"species": "dog",
		"sex": "m",
		"size": "medium",
		"img": "https://uploaddeimagens.com.br/images/003/866/664/original/cao2_1.png",
		"moreInfo": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
		"id": 2
	},
]
```

---

### **Listar animal por id:**

method: GET

endpoint: /644/animals/:id

body: empty

<br>**Exemplo de respostas:**

exemplo de endpoint: .../644/animals/1

```
{
	"userId": 1,
	"name": "fiona",
	"species": "dog",
	"sex": "f",
	"size": "small",
	"img": "https://uploaddeimagens.com.br/images/003/866/666/original/cao1_1.png",
	"moreInfo": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ac nibh ut felis scelerisque finibus sit amet in tortor. ",
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

exemplo de endpoint: .../644/animals?species=dog

```
[
	{
		"userId": 1,
		"name": "fiona",
		"species": "dog",
		"sex": "f",
		"size": "small",
		"img": "https://uploaddeimagens.com.br/images/003/866/666/original/cao1_1.png",
		"moreInfo": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ac nibh ut felis scelerisque finibus sit amet in tortor. ",
		"id": 1
	},
	{
		"userId": 1,
		"name": "maxx",
		"species": "dog",
		"sex": "m",
		"size": "medium",
		"img": "https://uploaddeimagens.com.br/images/003/866/664/original/cao2_1.png",
		"moreInfo": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
		"id": 2
	},
]
```

---

### **Listar animal por usuário:**

method: GET

endpoint: /644/animals?userId=:id

body: empty

<br>**Exemplo de respostas:**

exemplo de endpoint: .../644/animals?userId=1

```
[
	{
		"userId": 1,
		"name": "fiona",
		"species": "dog",
		"sex": "f",
		"size": "small",
		"img": "https://uploaddeimagens.com.br/images/003/866/666/original/cao1_1.png",
		"moreInfo": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ac nibh ut felis scelerisque finibus sit amet in tortor. ",
		"id": 1
	},
	{
		"userId": 1,
		"name": "maxx",
		"species": "dog",
		"sex": "m",
		"size": "medium",
		"img": "https://uploaddeimagens.com.br/images/003/866/664/original/cao2_1.png",
		"moreInfo": "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
		"id": 2
	},
]
```

---

### **Editar animal pelo id:**

method: PATCH

endpoint: /644/animals/:id

authentication (bearer): token do usuário que cadastrou o animal

body:

```
{
	"name":"fionna"
}
```

<br>**Exemplo de respostas:**

exemplo de endpoint: .../644/animals/1

se a propriedade existe no objeto:

```
{
		"userId": 1,
		"name": "fionna",
		"species": "dog",
		"sex": "f",
		"size": "small",
		"img": "https://uploaddeimagens.com.br/images/003/866/666/original/cao1_1.png",
		"moreInfo": "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras ac nibh ut felis scelerisque finibus sit amet in tortor. ",
		"id": 1
	},
```

**Nota:** se a propriedade não existir, será criada uma nova propriedade com o nome e valor que foram enviados.

---

### **Deletar animal pelo id:**

method: DELETE

endpoint: /644/animals/:id

authentication (bearer): token do usuário que cadastrou o animal

body: empty

<br>**Exemplo de respostas:**

exemplo de endpoint: ...644/animals/1

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
