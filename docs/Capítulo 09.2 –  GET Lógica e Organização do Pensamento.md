# 🧠 GET – Lógica e Organização do Pensamento

> 🎯 **Objetivo**: Antes de escrever qualquer linha de código, entenda a lógica por trás de um endpoint do tipo `GET` e por que ele é fundamental em uma API REST.

---

## 🧩 9.2.1. Qual é a função de um GET?

O método `GET` é utilizado quando precisamos **consultar ou buscar informações** em um sistema.  
Ele **não altera nada**, apenas **lê dados** existentes.

### 📚 Exemplos práticos:
- Ver a lista de usuários cadastrados
- Ver os detalhes de uma tarefa
- Consultar produtos disponíveis em uma loja

---

## 🧠 9.2.2. O que esse endpoint precisa fazer?

Vamos criar dois endpoints do tipo `GET`:
1. Listar todos os usuários
2. Buscar um único usuário por ID

---

## 🔁 9.2.3. Qual é o fluxo lógico de um GET?

### 📝 Para `GET /usuarios` (listar todos):

1. Receber uma requisição
2. Acessar a lista de usuários (mock ou banco)
3. Retornar todos os dados com status `200`

---

### 🔍 Para `GET /usuarios/:id` (buscar um):

1. Receber a requisição com um ID na URL
2. Verificar se o ID existe na lista
3. Se existir:
   - Retornar o usuário com status `200`
4. Se **não** existir:
   - Retornar erro com status `404` e mensagem de "Usuário não encontrado"

---

## 🛠️ 9.2.4. Por que usamos `GET` e não outro método?

| Método  | Quando usar                        |
|---------|------------------------------------|
| `GET`   | Quando **apenas queremos consultar** dados, sem alterar nada |
| `POST`  | Quando queremos **criar** algo novo |
| `PUT`   | Quando vamos **atualizar** algo existente |
| `DELETE`| Quando queremos **remover** um item |

> 💡 Usar o método certo faz parte do design inteligente da API.

---

## 📋 9.2.5. O que precisamos validar?

### No `GET /usuarios`:
- Nenhuma validação: apenas retornar tudo

### No `GET /usuarios/:id`:
- Validar se o ID é **um número**
- Validar se existe alguém com esse ID
- Se não existir, retornar uma mensagem de erro (`404`)

---

## 📤 9.2.6. O que o sistema deve retornar?

### ✅ Em caso de sucesso:

```json
{
  "success": true,
  "data": {
    "id": 2,
    "nome": "Maria Souza",
    "email": "maria@email.com"
  }
}
```

### ❌ Em caso de erro:

```json
{
  "success": false,
  "error": "Usuário não encontrado!"
}
```

---

## 🔍 9.2.7. Analisando a estrutura do `app.get()`

### 📌 Sintaxe:

```javascript
app.get('/usuarios', (req, res) => {
  res.status(200).json({ success: true, data: mockUsuarios });
});
```

### 🧠 Explicação lógica detalhada:

- **`app`** → é a instância da aplicação Express. É por onde tudo na API acontece: definição de rotas, uso de middlewares, inicialização do servidor.
- **`get()`** → é um método da instância `app`, que registra uma **rota do tipo GET**. Ou seja, uma rota que serve para **consultar dados**.
- **`'/usuarios'`** → é o caminho da URL que a API vai reconhecer. Quando o navegador ou o Thunder Client acessarem `/usuarios`, o Express saberá que é essa a função que deve ser executada.
- **`(req, res)`** → é uma função de callback. Ela é chamada quando essa rota é acionada.
  - `req` = **requisição** → traz informações da solicitação feita pelo cliente (como parâmetros, corpo, cabeçalhos, etc.).
  - `res` = **resposta** → é o que o servidor envia de volta para o cliente.
- **`res.status(200)`** → define o código de status HTTP que será retornado. `200` significa “requisição bem-sucedida”.
- **`.json({...})`** → envia a resposta no formato JSON, o mais utilizado em APIs REST.
- **`success: true`** → valor booleano que indicamos para dizer que a resposta foi um sucesso (pode ser usado pelo frontend para confirmar isso).
- **`data: mockUsuarios`** → os dados reais que estamos retornando: nesse caso, um array com todos os usuários cadastrados no mock.

---

## 🧠 9.2.8. Como esse endpoint se encaixa no sistema?

Todo sistema precisa **mostrar dados**.  
O `GET` é o que conecta o **frontend** (quem usa o sistema) ao **backend** (quem guarda os dados).  
Sem `GET`, o usuário não consegue ver **nada**.

---

## 📝 9. Antes de codar, pense:

1. O que quero buscar?
2. Preciso de algum parâmetro?
3. Preciso validar algo?
4. O que retorno se der certo?
5. E se der errado?

> 👨‍💻 **Quando você sabe o que está fazendo, o código vem naturalmente depois.**

---

## 📚 9.2.9 Referências Complementares

- [Pensando antes de codar – Lógica com Node.js (YouTube)](https://www.youtube.com/watch?v=O0lgK5QoHlg)
- [Fluxo de requisição e resposta – Blog Rocketseat](https://blog.rocketseat.com.br/fluxo-de-requisicoes-no-nodejs/)
- [Como planejar um endpoint REST – Dev.to](https://dev.to/ruanmartinelli/planeje-suas-rotas-rest-com-express-1fa2)
- [Requisição GET passo a passo – Alura](https://cursos.alura.com.br/forum/topico-requisicao-get-passo-a-passo-124998)

---

⬅️ [Capítulo 09.1 – Entendendo o Método HTTP GET](<Capítulo 09.1 – Entendendo o Método HTTP GET.md>) | [🏠 Voltar à Home](<README.md>) | [Capítulo 09.3 – Criando Endpoints GET com Mocks ➡️](<Capítulo 09.3 – Criando Endpoints GET.md>)
