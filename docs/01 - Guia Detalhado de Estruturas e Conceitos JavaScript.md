# 📘 Conceitos de JavaScript Aplicados no Backend

> 🎯 **Objetivo**: Apresentar de forma textual, ampla e detalhada os principais conceitos de JavaScript utilizados no desenvolvimento backend com Node.js e Express, com foco especial nas estruturas de dados, métodos de arrays, objetos e manipulações comuns ao CRUD.

---

## 🧱 1. Arrays em JavaScript

### 🔎 O que é um Array?

Um **array** é uma estrutura de dados que permite armazenar vários valores em uma única variável.  
Cada item possui um índice numérico (baseado em zero), permitindo o acesso direto aos dados.

```js
const numeros = [10, 20, 30];
console.log(numeros[0]); // 10
```

### 📦 Por que usamos arrays?

No backend, usamos arrays para representar **listas de dados** — por exemplo, uma lista de usuários, tarefas, produtos, etc.

---

### 🔧 Métodos importantes de arrays:

#### `.push(item)`

Adiciona um item ao final do array.

```js
const usuarios = [];
usuarios.push({ id: 1, nome: "Lucas" });
```

#### `.find(callback)`

Retorna o **primeiro item** que satisfaz a condição.  
Ideal para **buscar um único elemento**, como um usuário por ID.

```js
const usuario = usuarios.find(u => u.id === 1);
```

#### `.findIndex(callback)`

Retorna o **índice** do item no array que satisfaz a condição.  
É útil quando você precisa atualizar ou remover algo com base na posição.

```js
const index = usuarios.findIndex(u => u.id === 1);
```

#### `.some(callback)`

Verifica se **existe ao menos um item** que satisfaça a condição.  
Retorna um valor booleano (`true` ou `false`).

```js
const existe = usuarios.some(u => u.email === "teste@email.com");
```

#### `.splice(inicio, quantidade)`

Remove ou substitui itens do array a partir de um índice.

```js
usuarios.splice(1, 1); // remove 1 item a partir do índice 1
```

---

## 🧰 2. Objetos

### 🔎 O que é um objeto?

Um objeto é uma coleção de **pares chave-valor**, usados para representar **entidades** com atributos.

```js
const usuario = {
  id: 1,
  nome: "Ana",
  email: "ana@email.com"
};
```

### 📌 Por que usar objetos?

- Representam **estruturas complexas** como um usuário, tarefa, ou produto.
- Permitem agrupar dados relacionados sob uma única variável.

---

### 🧠 Acessando e modificando objetos:

```js
console.log(usuario.nome);       // 'Ana'
usuario.email = "novo@email.com";
```

---

### 🔄 Spread operator (`...`)

Permite **clonar e modificar objetos** de forma limpa e moderna.

```js
const atualizado = {
  ...usuario,
  nome: "Ana Maria"
};
```

> Muito utilizado em atualizações (método PUT) para manter campos existentes e sobrescrever apenas os novos.

---

## 🔄 3. Funções anônimas e arrow functions

### 🔎 O que são?

São funções que não possuem nome e geralmente são passadas como argumentos para outros métodos.

```js
const saudacao = () => {
  console.log("Olá, mundo!");
};
```

No Express, usamos muito esse formato para definir comportamentos de rotas:

```js
app.get('/usuarios', (req, res) => {
  res.send('Listando usuários');
});
```

---

## 📥 4. `req.params`, `req.body` e `req.query`

### `req.params`

- Contém **parâmetros de rota** definidos com `:` na URL.
- Ex: `/usuarios/:id`

```js
router.get('/usuarios/:id', (req, res) => {
  const id = req.params.id;
});
```

### `req.body`

- Contém os dados enviados no corpo da requisição (`POST` e `PUT`).
- Requer o middleware `express.json()` para funcionar.

```js
app.use(express.json());
router.post('/usuarios', (req, res) => {
  const { nome, email } = req.body;
});
```

### 🔸 `req.query`

- Contém **parâmetros opcionais enviados na URL**, geralmente usados para **filtros ou paginação**.
- Muito utilizado para filtros e paginações.

#### 📌 Exemplo de URL com query string:

```
GET /usuarios?nome=Ana&limite=10
```

```js
router.get('/usuarios', (req, res) => {
  const { nome, limite } = req.query;

  // nome === "Ana"
  // limite === "10" (atenção: tudo chega como string)

  res.json({ nome, limite });
});
```

📌 Exemplo de uso:

```js
router.get('/produtos', (req, res) => {
  const categoria = req.query.categoria;
  const ordem = req.query.ordem;

  res.send(`Filtrando produtos por ${categoria}, ordenados por ${ordem}`);
});
```

- Rota chamada com `/produtos?categoria=livros&ordem=preco`
  - `req.query.categoria === "livros"`
  - `req.query.ordem === "preco"`

> 🔎 Dica: o conteúdo de `req.query` **sempre será um objeto com valores em formato de texto (string)**. Use `parseInt()` ou `Number()` se precisar de números.


- Contém os dados enviados no corpo da requisição (`POST` e `PUT`).
- Requer o middleware `express.json()` para funcionar.

```js
app.use(express.json());
router.post('/usuarios', (req, res) => {
  const { nome, email } = req.body;
});
```

✅ **Vantagens de `req.query`:**

- Permite adicionar filtros sem alterar a rota
- Ideal para busca avançada (ex: `/tarefas?concluida=true`)
- Mais flexível e não obriga estrutura rígida

---

🔍 **Resumo**:

| Tipo         | Origem                       | Exemplo de uso                                |
| ------------ | ---------------------------- | --------------------------------------------- |
| `req.params` | URL com parâmetro de rota    | `/usuarios/:id`                               |
| `req.body`   | Corpo da requisição (JSON)   | `{ "nome": "Lucas", "email": "x@email.com" }` |
| `req.query`  | Query string após `?` na URL | `/produtos?categoria=livros&ordem=preco`      |

---

## 📤 5. Métodos de resposta (`res`)

| Método             | Função                                 |
|--------------------|----------------------------------------|
| `res.status(n)`    | Define o código de status HTTP         |
| `res.json(obj)`    | Envia uma resposta em JSON             |
| `res.send(texto)`  | Envia texto puro                       |
| `res.end()`        | Finaliza a resposta sem corpo          |

---

## ⚙️ 6. Operadores lógicos comuns

### `&&` – E lógico

Executa o segundo comando se o primeiro for verdadeiro.

```js
idade > 18 && console.log("Maior de idade");
```

### `||` – OU lógico

Executa o segundo valor se o primeiro for falso.

```js
const nome = entrada || "Anônimo";
```

### `!` – Negação

Inverte um valor booleano.

```js
if (!usuario) {
  console.log("Usuário não existe");
}
```

---

## 📦 7. Desestruturação

Permite extrair valores de objetos de forma prática.

```js
const usuario = { nome: "Carlos", email: "carlos@email.com" };
const { nome, email } = usuario;
```

---

## 🗓️ 8. Manipulação de datas

### Criar a data atual no formato padrão ISO:

```js
const data = new Date().toISOString(); 
```

### Formatar para apenas a data:

```js
const dataFormatada = new Date().toISOString().split('T')[0];
// Resultado: '2025-04-18'
```

---

## 🔁 9. Controle de fluxo com `if`

```js
if (!nome || !email) {
  return res.status(400).json({ error: "Dados obrigatórios" });
}
```

- Testa condições antes de continuar.
- Impede que dados inválidos avancem no código.

---

## 🔤 10. Strings em JavaScript – Conceito e Manipulação

### 🧠 O que é uma string?

Uma **string** é uma sequência de caracteres — ou seja, um **texto**.  
Em JavaScript, strings podem conter letras, números, símbolos e espaços.

```js
const nome = "Maria";
const saudacao = 'Olá, mundo!';
const frase = `Bem-vindo, ${nome}`; // template string
```

> 💡 Strings são **valores muito comuns em sistemas web**, e são a base da maioria das informações trocadas entre frontend e backend.

------

### 🧩 Como declarar strings?

Você pode usar três formas:

```js
const a = "Texto entre aspas duplas";
const b = 'Texto entre aspas simples';
const c = `Texto com crase (template string)`;
```

> ✅ **Template strings** (com crase) permitem **interpolação de variáveis**:

```js
const nome = "João";
console.log(`Olá, ${nome}!`); // Olá, João!
```

------

### 🔗 Concatenação de strings

**Concatenar** significa **juntar textos**:

```js
const nome = "Carlos";
const mensagem = "Bem-vindo, " + nome + "!";
console.log(mensagem); // Bem-vindo, Carlos!
```

> ⚠️ Este formato é antigo. Hoje preferimos:

```js
const mensagem = `Bem-vindo, ${nome}!`;
```

------

## 🧰 Métodos úteis para manipulação de strings

### `.length`

Retorna o número de caracteres:

```js
const texto = "Olá";
console.log(texto.length); // 3
```

------

### `.toUpperCase()` / `.toLowerCase()`

Transforma em **maiúsculo** ou **minúsculo**:

```js
const palavra = "Express";
console.log(palavra.toUpperCase()); // "EXPRESS"
console.log(palavra.toLowerCase()); // "express"
```

------

### `.trim()`

Remove espaços **antes e depois** da string:

```js
const nome = "   Lucas   ";
console.log(nome.trim()); // "Lucas"
```

------

### `.includes()`

Verifica se uma substring está presente:

```js
const frase = "API de usuários";
console.log(frase.includes("usuários")); // true
```

------

### `.startsWith()` / `.endsWith()`

Verifica se começa ou termina com certo texto:

```js
const arquivo = "relatorio.pdf";
console.log(arquivo.endsWith(".pdf")); // true
```

------

### `.slice(início, fim)`

Extrai parte da string:

```js
const texto = "JavaScript";
console.log(texto.slice(0, 4)); // "Java"
```

------

### `.replace(busca, substituto)`

Substitui uma parte do texto:

```js
const frase = "Olá, usuário!";
console.log(frase.replace("usuário", "admin")); // "Olá, admin!"
```

------

### `.split(separador)`

Divide uma string em partes, retornando um array:

```js
const frase = "nome=email@teste.com";
const partes = frase.split("=");
// partes = ["nome", "email@teste.com"]
```

------

## 🔎 Aplicações práticas no backend com Express

### 🔹 1. Filtro com `includes()` no `req.query`

```js
router.get('/usuarios', (req, res) => {
  const { nome } = req.query;

  const resultado = mockUsuarios.filter(usuario =>
    usuario.nome.toLowerCase().includes(nome.toLowerCase())
  );

  res.json({ success: true, data: resultado });
});
```

> 📌 Aqui o usuário pode acessar:
>
> ```
> GET /usuarios?nome=ana
> ```

------

### 🔹 2. Tratando espaços com `.trim()` e comparações seguras

```js
const busca = req.query.nome?.trim().toLowerCase();
```

------

## ✅ Observação

Strings são o tipo de dado **mais usado em APIs**.
 Saber manipulá-las corretamente permite que o backend:

- Valide entradas
- Filtros por nome ou email
- Trate URLs dinâmicas com segurança
- Responda com clareza e controle total

> 📚 Dominar os métodos de string é essencial para criar APIs REST robustas, flexíveis e inteligentes.

---

## 🧠 Conclusão

Esses conceitos de JavaScript são os pilares do desenvolvimento backend com Express.  
Ao dominá-los, o aluno ganha segurança para entender, adaptar e escrever seus próprios códigos.

> 📚 Este material pode ser usado como consulta rápida durante o desenvolvimento e para revisão antes de avaliações.

---

---

## 📚 Referências Complementares

- [Documentação oficial do JavaScript (MDN – em português)](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript)
- [Curso completo de JavaScript para iniciantes – Curso em Vídeo (YouTube)](https://www.youtube.com/playlist?list=PLHz_AreHm4dlFXCbtwTZ2hjQoaVg05D0H)
- [Conceitos fundamentais de objetos e arrays – Alura](https://www.alura.com.br/artigos/javascript-objetos-arrays)
- [Trabalhando com strings, datas e operadores – Dev.to](https://dev.to/rodrigokamada/javascript-trabalhando-com-strings-datas-e-operadores-30m7)
- [Spread, desestruturação e funções modernas em JS – Origamid](https://www.origamid.com/slide/javascript-avancado-es6/)

---

[🏠 Voltar à Home](<README.md>) | [02- ➡️](<docs/<>)
