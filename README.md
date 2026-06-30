# SalonTime — API Web Services

## Padrão de Retorno da API

Todos os endpoints da API do **SalonTime** seguem o mesmo padrão de resposta em JSON.

| Código | `status`                | Significado                              |
| ------ | ----------------------- | ---------------------------------------- |
| 200    | `success`               | Requisição realizada com sucesso.        |
| 201    | `created`               | Recurso criado com sucesso.              |
| 400    | `bad_request`           | Dados enviados inválidos ou incompletos. |
| 401    | `unauthorized`          | Usuário não autenticado.                 |
| 403    | `forbidden`             | Usuário autenticado, mas sem permissão.  |
| 404    | `not_found`             | Recurso não encontrado.                  |
| 500    | `internal_server_error` | Erro interno do servidor.                |

---

# Endpoint 01 — Listar Profissionais

## Contextualizando

Ao acessar o SalonTime, o cliente precisa visualizar todas as cabeleireiras cadastradas para escolher com quem deseja agendar um horário.

## Objetivo

Criar um endpoint que retorne todos os profissionais cadastrados.

### Endpoint

```http
GET /professionals
```

### Retorno

```json
{
  "code": 200,
  "type": "success",
  "status": "success",
  "message": "Lista de profissionais",
  "data": [
    {
      "id": 1,
      "name": "Maria Oliveira",
      "specialty": "Coloração"
    },
    {
      "id": 2,
      "name": "Ana Souza",
      "specialty": "Cortes Femininos"
    }
  ]
}
```

---

# Endpoint 02 — Listar Serviços

## Contextualizando

Depois de escolher a profissional, o cliente precisa visualizar todos os serviços disponíveis para realizar o agendamento.

## Objetivo

Retornar todos os serviços cadastrados.

### Endpoint

```http
GET /services
```

### Retorno

```json
{
  "code": 200,
  "type": "success",
  "status": "success",
  "message": "Lista de serviços",
  "data": [
    {
      "id": 1,
      "name": "Corte Feminino",
      "price": 60.00,
      "duration": 60
    },
    {
      "id": 2,
      "name": "Escova",
      "price": 45.00,
      "duration": 40
    }
  ]
}
```

---

# Endpoint 03 — Cadastrar Cliente

## Contextualizando

Antes de realizar um agendamento, o usuário precisa possuir um cadastro na plataforma.

## Objetivo

Cadastrar um novo cliente.

### Endpoint

```http
POST /clients
```

### Body

```json
{
  "name": "João Silva",
  "email": "joao@email.com",
  "password": "123456"
}
```

### Sucesso

```json
{
  "code": 201,
  "type": "success",
  "status": "created",
  "message": "Cliente cadastrado com sucesso",
  "data": {
    "id": 15,
    "name": "João Silva",
    "email": "joao@email.com"
  }
}
```

### Erro

```json
{
  "code": 400,
  "type": "error",
  "status": "bad_request",
  "message": "Todos os campos são obrigatórios",
  "data": null
}
```

---

# Endpoint 04 — Realizar Agendamento

## Contextualizando

Após efetuar login, o cliente poderá escolher o profissional, o serviço, a data e o horário disponíveis.

## Objetivo

Cadastrar um novo agendamento.

### Endpoint

```http
POST /appointments
```

### Body

```json
{
  "client_id": 1,
  "professional_id": 2,
  "service_id": 3,
  "date": "2026-06-20",
  "time": "14:00"
}
```

### Sucesso

```json
{
  "code": 201,
  "type": "success",
  "status": "created",
  "message": "Agendamento realizado com sucesso",
  "data": {
    "id": 32,
    "date": "2026-06-20",
    "time": "14:00"
  }
}
```

### Horário indisponível

```json
{
  "code": 400,
  "type": "error",
  "status": "bad_request",
  "message": "Horário indisponível",
  "data": null
}
```

---

# Endpoint 05 — Meus Agendamentos

## Contextualizando

Depois de realizar um agendamento, o cliente pode consultar todos os seus horários marcados.

## Objetivo

Retornar todos os agendamentos do cliente autenticado.

### Endpoint

```http
GET /appointments/my
```

### Sucesso

```json
{
  "code": 200,
  "type": "success",
  "status": "success",
  "message": "Meus agendamentos",
  "data": [
    {
      "id": 12,
      "professional": "Maria Oliveira",
      "service": "Coloração",
      "date": "2026-06-20",
      "time": "14:00",
      "status": "Confirmado"
    }
  ]
}
```

---

# Endpoint 06 — Cancelar Agendamento

## Contextualizando

Caso o cliente não possa comparecer, ele poderá cancelar seu horário sem excluir o histórico.

## Objetivo

Cancelar um agendamento alterando seu status para **Cancelado**.

### Endpoint

```http
PUT /appointments/{appointmentId}/cancel
```

### Sucesso

```json
{
  "code": 200,
  "type": "success",
  "status": "success",
  "message": "Agendamento cancelado com sucesso",
  "data": null
}
```

### Agendamento não encontrado

```json
{
  "code": 404,
  "type": "error",
  "status": "not_found",
  "message": "Agendamento não encontrado",
  "data": null
}
```

---

# Tecnologias Utilizadas

* PHP
* MySQL
* CoffeeCode Router
* Composer
* API REST
* JSON
* JWT (Autenticação)

---

# Estrutura da API

```
api/
│── source/
│   ├── Config/
│   ├── Controller/
│   ├── Core/
│   ├── Models/
│   └── Support/
│
├── vendor/
├── composer.json
└── index.php
```
