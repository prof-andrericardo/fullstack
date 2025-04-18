# 🛠️ Capítulo 8 – Rotas e Endpoints da API TO-DO LIST

> 🎯 **Objetivo**: Aprender a criar rotas e endpoints para a API REST da To-Do List, utilizando dados simulados (mocks) para realizar as operações básicas do CRUD (Criar, Ler, Atualizar e Deletar) em usuários e tarefas.
>
> 🧑‍🎓 Público-alvo: Alunos do 3º ano do Ensino Médio Técnico em Informática

---

## 📍 8.1 – O que são Rotas e Endpoints?

Uma **rota** é o caminho que define qual ação será executada no backend quando uma requisição HTTP é recebida.

Um **endpoint** é a junção de:
- **um método HTTP** (GET, POST, PUT, DELETE)
- **uma rota (caminho)** (ex: `/usuarios`, `/tarefas/1`)

> Exemplo: `GET /usuarios` é um endpoint que busca a lista de usuários.

---

## 🧩 8.2 – Organização Didática

Neste capítulo, vamos trabalhar com dois grupos de dados:
- 👤 **Usuários** (`mockUsuarios.js`)
- 📋 **Tarefas** (`mockTarefas.js`)

E para cada um, vamos implementar os 4 endpoints principais do CRUD:
- **GET** (Buscar)
- **POST** (Criar)
- **PUT** (Atualizar)
- **DELETE** (Remover)

> Utilizaremos apenas dados mockados por enquanto, mas o funcionamento será muito parecido quando estivermos com o banco de dados real.

---

## 👥 8.3 – Endpoints para Usuários (`/usuarios`)

### 📄 `GET /usuarios`

Retorna todos os usuários cadastrados.

**Resposta esperada:**
```json
{
  "success": true,
  "data": [ /* lista de usuários */ ]
}
```

------

### 🔍 `GET /usuarios/:id`

Busca um único usuário pelo `id`.
Retorna erro 404 caso o usuário não exista.

**Exemplo de sucesso:**

```json
{
  "success": true,
  "data": {
    "id": 1,
    "nome": "João Silva",
    "email": "joao@email.com"
  }
}
```

**Erro esperado (usuário não encontrado):**

```json
{
  "success": false,
  "error": "Usuário não encontrado!"
}
```

------

### ➕ `POST /usuarios`

Cria um novo usuário.
 Campos obrigatórios: `nome`, `email`

**Exemplo de corpo da requisição (JSON):**

```json
{
  "nome": "Novo Usuário",
  "email": "novo@email.com"
}
```

**Resposta esperada:**

```json
{
  "success": true,
  "data": {
    "id": 3,
    "nome": "Novo Usuário",
    "email": "novo@email.com"
  }
}
```

------

### ✏️ `PUT /usuarios/:id`

Atualiza os dados de um usuário.
Campos enviados sobrescrevem os antigos.

**Corpo da requisição:**

```json
{
  "nome": "Maria Atualizada"
}
```

------

### ❌ `DELETE /usuarios/:id`

Remove um usuário do sistema.

**Resposta esperada (sem corpo):**

- Status: `204 No Content`

**Erro esperado:**

```json
{
  "success": false,
  "error": "Usuário não encontrado!"
}
```

------

## 🧾 8.4 – Endpoints para Tarefas (`/tarefas`)

### 📄 `GET /tarefas`

Retorna todas as tarefas cadastradas.

------

### 🔍 `GET /tarefas/:id`

Retorna uma tarefa específica, junto com os dados do usuário dono da tarefa.

**Resposta esperada:**

```json
{
  "success": true,
  "data": {
    "id": 1,
    "titulo": "Estudar JS",
    "concluida": false,
    "usuario": {
      "id": 1,
      "nome": "João Silva"
    }
  }
}
```

------

### ➕ `POST /tarefas`

Cria uma nova tarefa vinculada a um usuário.

**Corpo da requisição:**

```json
{
  "titulo": "Nova tarefa",
  "usuario_id": 1,
  "descricao": "Exemplo"
}
```

> ⚠️ Deve verificar se o `usuario_id` informado existe.

------

### ✏️ `PUT /tarefas/:id`

Atualiza os dados de uma tarefa.
 Pode atualizar `titulo`, `descricao`, `concluida`, `usuario_id`, etc.

------

### ❌ `DELETE /tarefas/:id`

Remove uma tarefa.
 Retorna `204 No Content` se bem-sucedido, ou `404` se a tarefa não existir.

------

## 🧪 8.5 – Testando com Thunder Client

### 🔧 Dicas para testar

1. Instale a extensão **Thunder Client** no VSCode
2. Crie uma **coleção chamada "To-Do List API"**
3. Adicione as seguintes requisições:
   - `GET /usuarios`
   - `GET /usuarios/1`
   - `POST /usuarios`
   - `PUT /usuarios/1`
   - `DELETE /usuarios/1`
   - (repita para `/tarefas`)
4. Use `Content-Type: application/json` no cabeçalho dos métodos `POST` e `PUT`

------

### ✅ Dica visual de resposta

Verifique no Thunder Client:

| Item                     | O que deve aparecer                    |
| ------------------------ | -------------------------------------- |
| Status                   | 200, 201, 204, 404 ou 400              |
| Corpo da resposta        | JSON com `success` e `data` ou `error` |
| Terminal VSCode (morgan) | Logs das requisições com tempo         |

------

## 📘 8.6 – Boas Práticas para Rotas REST

| Boas práticas                      | Por quê?                                                |
| ---------------------------------- | ------------------------------------------------------- |
| Usar nomes no plural (`/usuarios`) | Segue padrão REST                                       |
| Incluir o ID diretamente na rota   | Evita ambiguidade e facilita leitura (`/tarefas/1`)     |
| Retornar status adequados          | Melhora integração com o frontend                       |
| Validar campos obrigatórios        | Garante consistência e evita erros de lógica            |
| Padronizar respostas em JSON       | Facilita testes, debug e consumo pela interface cliente |

------

## 💡 8.7 – Dica Profissional

> “APIs bem projetadas são aquelas que se comportam como um restaurante eficiente: entendem o pedido, entregam a resposta certa, informam quando algo dá errado e são fáceis de usar por quem está do outro lado.”

------

## 🧠 8.8 – Atividade Prática

> 🎯 **Objetivo**: Consolidar o uso dos métodos HTTP criando e testando todos os endpoints.

### 📌 Tarefa:

1. Teste todos os endpoints disponíveis com dados reais via Thunder Client
2. Crie uma tarefa fictícia vinculada a um usuário existente
3. Tente:
   - Atualizar uma tarefa com um `usuario_id` inválido
   - Excluir uma tarefa que já foi excluída
4. Anote os status HTTP de cada operação e interprete as respostas JSON

---

## 📚 8.9 Referências Complementares

- [Definindo rotas no Express – Documentação oficial](https://expressjs.com/pt-br/guide/routing.html)
- [O que são rotas e endpoints – YouTube (Tiago Matos)](https://www.youtube.com/watch?v=LDx0-QJdQnM)
- [Boas práticas em rotas REST – Dev.to](https://dev.to/telesdev/api-rest-com-boas-praticas-37dh)
- [Rotas dinâmicas com Express – Medium](https://medium.com/@programador.cs/rotas-din%C3%A2micas-e-est%C3%A1ticas-com-node-js-e-express-4b539e9273f9)

---

## 📚 Próximo Capítulo

➡️ Agora que implementamos todos os endpoints principais do CRUD usando dados mockados, vamos dar um passo atrás e compreender melhor o funcionamento de cada **método HTTP** em APIs REST.

No próximo capítulo, vamos estudar em profundidade o método `GET`, que é responsável pela **leitura de dados** em sistemas web.

Continue para: **[Capítulo 9.1 – Entendendo o Método HTTP GET](docs/<Capítulo 9.1 – Entendendo o Método HTTP GET.md>)**

------

⬅️ [Capítulo 07 – Conceitos Fundamentais de HTTP](<Capítulo 07 – Conceitos Fundamentais de HTTP.md>) | [🏠 Voltar à Home](<README.md>) | [Capítulo 09.0 – Explorando o Express e a Instância `app` ➡️](<Capítulo 09.0 – Explorando o Express e a Instância `app`.md>)
