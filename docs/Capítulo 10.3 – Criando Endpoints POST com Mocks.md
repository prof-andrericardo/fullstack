# 🧪 Capítulo 10.3 – Criando Endpoints POST com Mocks

> 🎯 **Objetivo**: Implementar endpoints `POST` para criar novos usuários e tarefas utilizando dados mockados. Este capítulo aplica os conceitos abordados no Capítulo 10.1 de forma prática e detalhada.
>
> 👨‍🎓 Público-alvo: Alunos do 3º ano do Ensino Médio Técnico em Informática

---

## 📦 10.3.1 – Estrutura esperada dos arquivos

Antes de começar, verifique se os seguintes arquivos estão organizados corretamente:

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

------

## 👤 10.3.2 – Endpoint: `POST /usuarios`

Este endpoint cria um novo usuário e adiciona no array `mockUsuarios`.

### 📌 Etapas da lógica:

1. Receber `nome` e `email` no `body` da requisição
2. Verificar se ambos os campos foram enviados
3. Gerar um novo `id` baseado no tamanho do array
4. Criar o novo usuário
5. Retornar o usuário criado com status `201 Created`

### ✅ Código:

```javascript
// Rota que cria um novo usuário
router.post('/usuarios', (req, res) => {
  const { nome, email } = req.body; // Extrai dados do corpo da requisição

  // Validação: nome e email são obrigatórios
  if (!nome || !email) {
    return res.status(400).json({
      success: false,
      error: 'Nome e email são obrigatórios!'
    });
  }

  // Cria novo objeto de usuário com ID gerado automaticamente
  const novoUsuario = {
    id: mockUsuarios.length + 1,
    nome,
    email
  };

  // Adiciona o novo usuário ao array de mocks
  mockUsuarios.push(novoUsuario);

  // Retorna o novo usuário criado com status 201
  res.status(201).json({
    success: true,
    data: novoUsuario
  });
});
```

**🔍 Explicação:**

- `req.body`: contém os dados enviados pelo cliente via JSON
- Verificamos se `nome` e `email` foram preenchidos
- O `id` é criado com base no tamanho atual do array
- `push()` insere o novo usuário no mock
- `status(201)` indica que algo foi criado com sucesso

------

## ✅ Exemplo de teste (Thunder Client):

- **URL**: `POST http://localhost:3000/usuarios`
- **Header**:
  - `Content-Type: application/json`
- **Body (JSON)**:

```json
{
  "nome": "Ana Clara",
  "email": "ana@exemplo.com"
}
```

- **Resposta esperada**: status `201`, objeto criado com novo `id`

------

## 📋 10.3.3 – Endpoint: `POST /tarefas`

Cria uma nova tarefa vinculada a um usuário já existente.

### 📌 Campos esperados no body:

- `titulo` (obrigatório)
- `descricao` (opcional)
- `usuario_id` (obrigatório e deve existir)

------

### ✅ Código:

```javascript
// Rota que cria uma nova tarefa vinculada a um usuário
router.post('/tarefas', (req, res) => {
  const { titulo, descricao, usuario_id } = req.body;

  // Verifica se os campos obrigatórios foram enviados
  if (!titulo || !usuario_id) {
    return res.status(400).json({
      success: false,
      error: 'Título e ID do usuário são obrigatórios!'
    });
  }

  // Verifica se o usuário informado realmente existe
  const usuarioExiste = mockUsuarios.some(u => u.id === usuario_id);
  if (!usuarioExiste) {
    return res.status(404).json({
      success: false,
      error: 'Usuário não encontrado!'
    });
  }

  // Cria nova tarefa com dados enviados + campos padrão
  const novaTarefa = {
    id: mockTarefas.length + 1,
    titulo,
    descricao: descricao || '',
    concluida: false,
    usuario_id,
    criado_em: new Date().toISOString().split('T')[0] // data no formato yyyy-mm-dd
  };

  // Adiciona no mock de tarefas
  mockTarefas.push(novaTarefa);

  // Retorna a nova tarefa com status 201
  res.status(201).json({
    success: true,
    data: novaTarefa
  });
});
```

**🔍 Explicação:**

- Validação dos campos obrigatórios (`titulo`, `usuario_id`)
- `some()` verifica se há algum usuário com o ID informado
- Criamos um objeto `novaTarefa` com um novo `id`, status `concluida: false` e data atual
- O objeto é inserido com `push()` no mock
- A resposta é retornada com `201 Created`

------

### 🧪 Teste com Thunder Client:

- **URL**: `POST http://localhost:3000/tarefas`
- **Body**:

```json
{
  "titulo": "Finalizar projeto da API",
  "descricao": "Concluir todos os endpoints",
  "usuario_id": 2
}
```

- **Resposta esperada**: status `201` + objeto da nova tarefa

------

## ⚠️ 10.3.4 – Casos de erro importantes

| Cenário                         | Status esperado | Mensagem de erro                        |
| ------------------------------- | --------------- | --------------------------------------- |
| `nome` ou `email` ausente       | `400`           | Nome e email são obrigatórios           |
| `usuario_id` inválido em tarefa | `404`           | Usuário não encontrado                  |
| `titulo` ausente em tarefa      | `400`           | Título e ID do usuário são obrigatórios |

------

## 📘 10.3.5 – Boas práticas aplicadas

| Boas práticas observadas                 | Justificativa                              |
| ---------------------------------------- | ------------------------------------------ |
| Gerar `id` automaticamente               | Imita bancos reais com `AUTO_INCREMENT`    |
| Validar dados obrigatórios               | Evita corrupção ou falhas de dados         |
| Usar `status 201` corretamente           | Indica que o recurso foi criado            |
| Retornar objeto criado na resposta       | Ajuda o frontend a atualizar sua interface |
| Utilizar `descricao` como campo opcional | Flexibilidade para o usuário               |

------

## 🧠 10.3.6 – Atividade Prática

> **Objetivo**: Praticar a criação de dados via `POST` e refletir sobre o retorno da API.

### 📌 Desafio:

1. Crie **2 novos usuários** usando `POST /usuarios`
2. Em seguida, crie **3 tarefas** associadas a esses usuários
3. Faça um teste de erro:
   - Tente criar uma tarefa com `usuario_id` inexistente
   - Tente criar uma tarefa sem `titulo`
4. Anote os **status HTTP retornados** e a **mensagem de resposta** em cada caso

---

## 📚 Referências Complementares

- [Criando rotas POST com Express – W3Schools](https://www.w3schools.com/nodejs/nodejs_mysql_create_db.asp)
- [Tratando dados do `req.body` – Alura](https://www.alura.com.br/artigos/body-parser-express)
- [Exemplo prático de POST em APIs REST – YouTube (Programação Dinâmica)](https://www.youtube.com/watch?v=LUvUBqurjD4)
- [Validando campos obrigatórios com Express](https://express-validator.github.io/docs/)

---

## 📚 Próximo Capítulo

Agora que você domina o método POST e sabe como criar recursos com segurança, vamos seguir para a **atualização de dados**, utilizando o método `PUT`.

➡️ Continue para: **[Capítulo 11.1 – Entendendo o Método PUT](docs/<Capítulo 11.1 – Entendendo o Método HTTP PUT.md>)**

------

⬅️ [Capítulo 10.2 – POST Lógica e Organização do Pensamento](<Capítulo 10.2 – POST Lógica e Organização do Pensamento.md>) | [🏠 Voltar à Home](<README.md>) | [Capítulo 11.1 – Entendendo o Método HTTP PUT ➡️](<Capítulo 11.1 – Entendendo o Método HTTP PUT.md>)
