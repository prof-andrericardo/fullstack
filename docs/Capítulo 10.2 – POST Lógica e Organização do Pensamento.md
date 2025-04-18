# 🧠 POST – Lógica e Organização do Pensamento

> 🎯 **Objetivo**: Compreender a lógica por trás de um endpoint do tipo `POST`, antes de escrever qualquer código. Ideal para alunos que estão aprendendo como criar dados de forma segura e validada.

---

## 📩 10.2.1. Qual é a função de um POST?

O método `POST` é utilizado para **criar um novo recurso** no sistema.  
Ele é o responsável por **adicionar dados** ao backend (em mocks ou banco de dados).

### 📚 Exemplos práticos:
- Criar um novo usuário
- Adicionar uma nova tarefa
- Fazer um cadastro de produto

---

## 🧠 10.2.2. O que esse endpoint precisa fazer?

Vamos criar dois endpoints do tipo `POST`:
1. Criar um novo usuário
2. Criar uma nova tarefa vinculada a um usuário

---

## 🔁 10.2.3. Qual é o fluxo lógico de um POST?

### 📝 Para `POST /usuarios`:

1. Receber uma requisição com `nome` e `email` no corpo (JSON)
2. Validar se os campos foram preenchidos
3. Gerar um novo ID
4. Criar um novo objeto com os dados recebidos
5. Adicionar esse objeto ao array de usuários
6. Retornar status `201 Created` e o objeto criado

---

### 📝 Para `POST /tarefas`:

1. Receber os dados da nova tarefa (`titulo`, `descricao`, `usuario_id`)
2. Validar se `titulo` e `usuario_id` foram enviados
3. Validar se o usuário existe
4. Criar a tarefa com os dados + status `concluida: false`
5. Adicionar ao array de tarefas
6. Retornar status `201` com a nova tarefa

---

## ⚙️ 10.2.4. Por que usamos `POST`?

| Método  | Quando usar                        |
|---------|------------------------------------|
| `POST`  | Quando vamos **criar algo novo**   |
| `GET`   | Quando queremos apenas consultar   |
| `PUT`   | Quando atualizamos algo existente  |
| `DELETE`| Quando queremos excluir um item    |

---

## 📋 10.2.5. O que precisamos validar?

- Se os campos obrigatórios foram enviados (`nome`, `email`, `titulo`, `usuario_id`)
- Se o `usuario_id` enviado na tarefa existe de fato
- Evitar aceitar dados incompletos ou inválidos

---

## 🧠 10.2.6. Entendendo a estrutura do `app.post()`

### 📌 Sintaxe:

```js
app.post('/usuarios', (req, res) => {
  const { nome, email } = req.body;

  if (!nome || !email) {
    return res.status(400).json({ success: false, error: 'Dados obrigatórios!' });
  }

  const novoUsuario = {
    id: mockUsuarios.length + 1,
    nome,
    email
  };

  mockUsuarios.push(novoUsuario);

  res.status(201).json({ success: true, data: novoUsuario });
});
```

---

### 🔍 Explicação lógica:

- **`app.post()`** → método do Express que cria uma **rota do tipo POST**
- **`'/usuarios'`** → caminho da rota (quem acessar isso com POST vai cair aqui)
- **`req.body`** → contém os dados enviados pelo cliente no corpo da requisição
- **Validação `if (!nome || !email)`** → impede que cadastros incompletos sejam aceitos
- **`mockUsuarios.length + 1`** → simula a geração de um novo ID
- **`mockUsuarios.push()`** → insere o novo usuário no array
- **`res.status(201)`** → indica que um recurso foi criado
- **`.json()`** → envia a resposta em formato JSON com o novo objeto

---

## 📤 10.2.7. O que o sistema deve retornar?

### ✅ Em caso de sucesso:

```json
{
  "success": true,
  "data": {
    "id": 3,
    "nome": "Lucas",
    "email": "lucas@email.com"
  }
}
```

### ❌ Em caso de erro:

```json
{
  "success": false,
  "error": "Nome e email são obrigatórios!"
}
```

---

## 📚 10.2.8. Como esse endpoint se encaixa no sistema?

Sem `POST`, o sistema **não pode crescer**.  
É por ele que os dados entram na aplicação: cadastros, formulários, uploads…  
É a **porta de entrada oficial de novas informações**.

---

## 📝 10.2.9. Antes de codar, pense:

1. O que preciso criar?
2. Quais campos são obrigatórios?
3. De onde virão os dados?
4. Preciso validar alguma regra de negócio?
5. O que retorno em caso de sucesso?
6. E se der erro?

> 👨‍💻 Quando você domina a lógica do POST, está preparado para qualquer cadastro!

---

## 📚 10.2.10 Referências Complementares

- [Planejando endpoints POST – Medium](https://medium.com/@lucasfeliciano/api-rest-planejando-endpoints-eficientes-df19ecfc9b4)
- [Como organizar o corpo (body) da requisição – Alura](https://www.alura.com.br/artigos/body-parser-express)
- [Pensando o fluxo de criação – Dev.to](https://dev.to/ruanmartinelli/planeje-suas-rotas-rest-com-express-1fa2)
- [Função push em arrays – MDN Docs (pt-BR)](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/push)

---

⬅️ [Capítulo 10.1 – Entendendo o Método HTTP POST](<Capítulo 10.1 – Entendendo o Método HTTP POST.md>) | [🏠 Voltar à Home](<README.md>) | [Capítulo 10.3 – Criando Endpoints POST com Mocks ➡️](<Capítulo 10.3 – Criando Endpoints POST com Mocks.md>)
