# 💻 Capítulo 9.2 – Criando Endpoints GET com Mocks

> 🎯 **Objetivo**: Implementar na prática os endpoints `GET` utilizando dados simulados com mocks. O foco será criar rotas REST que retornem **todos os registros** ou **um único item específico**.
>
> 🧑‍🎓 Público-alvo: Alunos do 3º ano do Ensino Médio Técnico em Informática

---

## 🧱 9.3.1 – Preparação do ambiente

Certifique-se de que os seguintes arquivos estão configurados corretamente:

### 📁 Estrutura esperada:

```plaintext
backend/
├── src/
│   ├── routes/
│   │   └── api.js
│   ├── mocks/
│   │   ├── mockUsuarios.js
│   │   └── mockTarefas.js
│   └── app.js
├── server.js
```

### 📦 Conteúdo de exemplo para `mockUsuarios.js`

```javascript
export default [
  {
    id: 1,
    nome: "João Silva",
    email: "joao@email.com"
  },
  {
    id: 2,
    nome: "Maria Souza",
    email: "maria@email.com"
  }
];
```

### 📦 Conteúdo de exemplo para `mockTarefas.js`

```javascript
export default [
  {
    id: 1,
    titulo: "Estudar Node.js",
    descricao: "Praticar middlewares",
    concluida: false,
    usuario_id: 1
  },
  {
    id: 2,
    titulo: "Comprar pão",
    descricao: "Padaria do bairro",
    concluida: true,
    usuario_id: 2
  }
];
```

------

## 🔧 9.3.2 – Importando os mocks e criando o router

### 📄 `src/routes/api.js`

```javascript
// Importa o roteador do Express
import { Router } from 'express';

// Importa os dados simulados (mocks)
import mockUsuarios from '../mocks/mockUsuarios.js';
import mockTarefas from '../mocks/mockTarefas.js';

// Cria uma instância de roteador
const router = Router();
```

------

## 🔗 9.3.3 – Conectando o router ao `app.js`

### 📄 `src/app.js`

No `src/app.js`, certifique-se de importar e usar o router:

```javascript
import express from 'express';
import cors from 'cors';
import morgan from 'morgan';
import router from './routes/api.js';

const app = express();

app.use(express.json());
app.use(cors());
app.use(morgan('dev'));

// Conecta todas as rotas definidas em `api.js`
app.use(router);

export default app;
```

---

## 👥 9.3.4 – Endpoint: `GET /usuarios`

Retorna a lista de todos os usuários.

```javascript
// Rota que retorna todos os usuários
router.get('/usuarios', (req, res) => {
  // Retorna os dados com status 200 (OK)
  res.status(200).json({
    success: true,
    data: mockUsuarios
  });
});
```

**🔍 Explicação:**

- `router.get('/usuarios', ...)`: define uma rota que responde a `GET /usuarios`
- `res.status(200)`: indica sucesso
- `res.json({ ... })`: envia uma resposta em formato JSON
- `mockUsuarios`: array com dados simulados de usuários

### ✅ Resultado esperado:

```json
{
  "success": true,
  "data": [
    { "id": 1, "nome": "João Silva", "email": "joao@email.com" },
    { "id": 2, "nome": "Maria Souza", "email": "maria@email.com" }
  ]
}
```

------

## 🔍 9.3.5 – Endpoint: `GET /usuarios/:id`

Retorna apenas o usuário com o `id` informado.

```javascript
// Rota que busca um usuário pelo ID
router.get('/usuarios/:id', (req, res) => {
  const id = parseInt(req.params.id); // Converte o ID da URL para número
  const usuario = mockUsuarios.find(u => u.id === id); // Procura o usuário no array

  if (!usuario) {
    // Se não encontrar, responde com erro 404
    return res.status(404).json({
      success: false,
      error: 'Usuário não encontrado!'
    });
  }

  // Se encontrar, retorna os dados com status 200
  res.status(200).json({
    success: true,
    data: usuario
  });
});
```

**🔍 Explicação:**

- `:id` é um parâmetro dinâmico na URL
- `parseInt()` transforma a string do ID em número
- `find()` busca o usuário pelo ID
- `404 Not Found` se o usuário não existir
- `200 OK` com os dados do usuário se encontrado

------

## 📋 9.3.6 – Endpoint: `GET /tarefas`

Retorna todas as tarefas da API.

```javascript
// GET /tarefas
router.get('/tarefas', (req, res) => {
  res.status(200).json({
    success: true,
    data: mockTarefas
  });
});
```

------

## 📌 9.3.7 – Endpoint: `GET /tarefas/:id`

Busca uma tarefa específica e também retorna os dados do usuário dono da tarefa.

```javascript
// Rota que busca uma tarefa por ID e retorna também o usuário dono
router.get('/tarefas/:id', (req, res) => {
  const id = parseInt(req.params.id); // ID da tarefa
  const tarefa = mockTarefas.find(t => t.id === id); // Busca a tarefa

  if (!tarefa) {
    return res.status(404).json({
      success: false,
      error: 'Tarefa não encontrada!'
    });
  }

  // Busca o usuário correspondente à tarefa
  const usuario = mockUsuarios.find(u => u.id === tarefa.usuario_id);

  res.status(200).json({
    success: true,
    data: {
      ...tarefa,       // Dados da tarefa
      usuario: usuario || null // Dados do usuário (ou null se não encontrado)
    }
  });
});
```

**🔍 Explicação:**

- Combina dados da tarefa e do usuário que criou a tarefa
- `...tarefa`: espalha todos os campos da tarefa
- `usuario || null`: garante que a chave "usuario" esteja presente, mesmo que vazia

**Obs.:** Adicione ao final do arquivo a exportação do `router`

```js
export default router;
```

------

## 🧪 9.3.8 – Testando com Thunder Client

### 📋 Endpoints para testar:

| Método | URL           | O que esperar                    |
| ------ | ------------- | -------------------------------- |
| GET    | `/usuarios`   | Lista com todos os usuários      |
| GET    | `/usuarios/1` | Dados do usuário de ID 1         |
| GET    | `/tarefas`    | Lista com todas as tarefas       |
| GET    | `/tarefas/2`  | Tarefa de ID 2 com dados do dono |

> 💡 Utilize `Content-Type: application/json` nas configurações do Thunder Client.

------

## ✅ 9.3.9 – Boas práticas aplicadas

- ✔️ Sempre verificar se o item existe antes de retornar
- ✔️ Utilizar `parseInt()` para converter `req.params.id`
- ✔️ Retornar `status 404` com mensagem amigável quando não encontrar o recurso
- ✔️ Utilizar `success: true` ou `false` para clareza nas respostas

------

## 🧠 9.3.10 – Atividade Prática

> **Objetivo**: Consolidar o uso do método GET criando e testando seus próprios endpoints.

### 📌 Desafio:

1. Crie dois novos registros em `mockUsuarios.js` e `mockTarefas.js`
2. Teste se os novos dados aparecem em:
   - `GET /usuarios`
   - `GET /tarefas`
   - `GET /tarefas/:id`
3. Adicione um novo campo `telefone` nos usuários e retorne esse dado no GET

---

## 📚 9.3.11 Referências Complementares

- [Express: Criando rotas GET – DevMedia](https://www.devmedia.com.br/express-node-js-criando-rotas/40485)
- [API REST com mocks e JSON – YouTube (Programação Dinâmica)](https://www.youtube.com/watch?v=LUvUBqurjD4)
- [Trabalhando com Express e dados simulados – Alura](https://www.alura.com.br/artigos/trabalhando-com-dados-node)
- [Documentação Express: `res.json()`](https://expressjs.com/en/api.html#res.json)

---

## 📚 Próximo Capítulo

Agora que você já sabe como criar endpoints `GET`, vamos avançar para o próximo verbo do CRUD:

➡️ Continue para: **[Capítulo 10.1 – Entendendo o Método POST](docs/<Capítulo 10.1 – Entendendo o Método HTTP POST.md>)**

------

⬅️ [Capítulo 09.2 – GET Lógica e Organização do Pensamento](<Capítulo 09.2 –  GET Lógica e Organização do Pensamento.md>) | [🏠 Voltar à Home](<../README.md>) | [Capítulo 10.1 – Entendendo o Método HTTP POST ➡️](<Capítulo 10.1 – Entendendo o Método HTTP POST.md>)
