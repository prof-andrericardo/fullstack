# 🚀 Capítulo 9 – Explorando o Express e a Instância `app`

> 🎯 **Objetivo**: Compreender o que é o Express, o papel da instância `app` e como seus métodos principais estruturam toda a aplicação backend em Node.js.
>
> 👨‍🎓 Público-alvo: Alunos do 3º ano do Ensino Médio Técnico em Informática

---

## 📘 9.1 – O que é o Express?

O **Express** é uma **biblioteca para Node.js** que facilita a criação de servidores web e APIs REST.  
Sem o Express, o Node.js puro exige que o desenvolvedor gerencie manualmente cada detalhe das requisições e respostas.

### 💡 Por que usar o Express?

- 📦 Simplifica a criação de rotas (`GET`, `POST`, `PUT`, `DELETE`)
- 🛠️ Permite usar middlewares (funções entre a requisição e a resposta)
- 🔧 Oferece ferramentas prontas para trabalhar com JSON, CORS, formulários etc.
- 💬 Facilita a leitura, manutenção e organização do código

---

## ⚙️ 9.2 – O que é `app`?

Ao escrever:

```javascript
import express from 'express';

const app = express();
```

Você está:

- Importando o **módulo Express**
- Criando uma **instância da aplicação Express**
- Guardando essa instância na variável `app`

> 🧠 O `app` é o **núcleo da aplicação**. É por meio dele que você:
>
> - Define rotas
> - Aplica middlewares
> - Controla o fluxo das requisições

🔎 **Observação – O que são Middlewares?**

Os **middlewares** são funções intermediárias que processam a requisição **antes** dela chegar na rota final ou **antes** de a resposta ser enviada ao cliente.

Eles podem:

- 📦 Adicionar informações ao objeto `req` (requisição)
- 🔐 Proteger rotas com autenticação
- 🧼 Validar dados
- 🧾 Registrar logs
- ⛔ Interromper o fluxo em caso de erro ou regra

### 📌 Exemplo comum:

```js
app.use(express.json()); // Middleware para interpretar JSON
```

> Nesse exemplo, toda requisição com corpo JSON será automaticamente interpretada antes de chegar nas rotas da API.

> 💡 Os middlewares são aplicados com `app.use()` ou diretamente em rotas específicas.

---

## 🧩 9.3 – Principais Métodos da Instância `app`

A seguir, conheça os principais métodos da instância `app` utilizados no desenvolvimento de APIs:

------

### 📍 9.3.1 – `app.use()`

Aplica **middlewares globais** à aplicação.

```javascript
app.use(express.json()); // Interpreta JSON
app.use(cors());         // Libera acesso externo
```

> 🧪 *Tudo que passar pela API será interceptado pelos middlewares definidos com `use()`.*

------

### 🔀 9.3.2 – `app.get()`, `app.post()`, `app.put()`, `app.delete()`

Usados para criar **rotas** que lidam com os diferentes tipos de requisições HTTP:

```javascript
app.get('/tarefas', (req, res) => { ... });
app.post('/usuarios', (req, res) => { ... });
```

> 🛣️ *Você está dizendo: “Quando alguém acessar essa rota com esse método, execute essa função.”*

------

### 🔚 9.3.3 – `app.listen()`

Inicializa o servidor e o coloca "ouvindo" uma porta.

```javascript
app.listen(3000, () => {
  console.log('Servidor rodando na porta 3000');
});
```

> 📡 *Sem esse comando, sua API não estará disponível.*

------

### 🛠️ 9.3.4 – `app.set()` (avançado)

Define variáveis de configuração da aplicação (ex: view engine, porta).

```javascript
app.set('view engine', 'ejs');
```

> 🔧 *Mais usado em projetos com páginas dinâmicas.*

------

### 🧪 9.3.5 – `app.engine()` (avançado)

Permite configurar como arquivos HTML serão renderizados.

> Usado em aplicações que entregam HTML ao cliente (não abordado neste projeto).

------

## ✅ **Métodos mais utilizados da instância `app` do Express**

### 🔝 Mais usados em **projetos backend RESTful com Express (Node.js)**:

| Método         | Descrição                                                    |
| -------------- | ------------------------------------------------------------ |
| `app.use()`    | Registra middlewares globais ou rotas modularizadas (`app.use('/api', ...)`) |
| `app.get()`    | Define uma rota que responde a requisições do tipo `GET`     |
| `app.post()`   | Define uma rota que responde a requisições do tipo `POST`    |
| `app.put()`    | Define uma rota que responde a requisições do tipo `PUT`     |
| `app.delete()` | Define uma rota que responde a requisições do tipo `DELETE`  |
| `app.listen()` | Inicia o servidor Express e define a porta de escuta         |
| `app.set()`    | Define variáveis de configuração da aplicação                |
| `app.engine()` | Configura um motor de template personalizado (útil para views HTML) |

------

### 📦 **Outros métodos úteis (em casos específicos ou avançados)**:

| Método          | Uso típico e relevância                                      |
| --------------- | ------------------------------------------------------------ |
| `app.all()`     | Define uma rota que responde a **todos os métodos HTTP**     |
| `app.route()`   | Encadeia múltiplos métodos HTTP na **mesma rota**            |
| `app.param()`   | Define middlewares específicos para parâmetros de rota       |
| `app.locals`    | Armazena variáveis globais para uso em templates/view (EJS, etc) |
| `app.disable()` | Desativa recursos internos do Express                        |
| `app.enable()`  | Ativa recursos que podem ser desativados por padrão          |
| `app.render()`  | Renderiza uma view, se estiver usando templates (HTML/EJS)   |

------

## 🔬 **Situações práticas de uso**

| Situação                                           | Método recomendado             |
| -------------------------------------------------- | ------------------------------ |
| Criar rotas REST comuns                            | `app.get()`, `app.post()` etc. |
| Criar middlewares globais e aplicar modularização  | `app.use()`                    |
| Encadear métodos HTTP na mesma rota                | `app.route()`                  |
| Reutilizar lógica para parâmetros (ex: `:id`)      | `app.param()`                  |
| Trabalhar com views HTML (ex: painel de admin)     | `app.set()`, `app.engine()`    |
| Testar API com todos os métodos para uma rota base | `app.all()`                    |

------

## 🔎 Observação

A lista que usamos no cobre os métodos **mais essenciais para o desenvolvimento de APIs RESTful modernas**, o que atende **90% dos projetos backend com Node.js e Express**.

No entanto, para uma formação **avançada e completa**, especialmente para alunos com interesse em aprofundamento, é **altamente recomendável apresentar também os métodos auxiliares**, como `app.route()`, `app.param()` e `app.all()` — mesmo que opcionalmente ou em um "apêndice de aprofundamento".

---

### 📚 Resumo da Função dos Métodos

| Método         | Para que serve                                     |
| -------------- | -------------------------------------------------- |
| `app.use()`    | Aplicar middlewares globais                        |
| `app.get()`    | Criar rota do tipo `GET`                           |
| `app.post()`   | Criar rota do tipo `POST`                          |
| `app.put()`    | Criar rota do tipo `PUT`                           |
| `app.delete()` | Criar rota do tipo `DELETE`                        |
| `app.listen()` | Iniciar o servidor                                 |
| `app.set()`    | Definir configurações internas (ex: porta, engine) |
| `app.engine()` | Configurar motores de template                     |

------

## 🧩 9.4 – Propriedades Importantes da instância `app`

> 🔍 **Introdução**:  
> Além dos métodos como `app.get()` e `app.use()`, a instância `app` do Express também possui **propriedades poderosas** que oferecem recursos adicionais, controle interno e flexibilidade no desenvolvimento de aplicações backend.

Estas propriedades são úteis tanto para projetos simples quanto para arquiteturas mais complexas, como aplicações modulares ou com motores de template.

---

## 📌 Propriedades úteis da instância `app`

---

### 🧱 9.4.1. `app.locals`

Permite armazenar **variáveis globais** da aplicação.

```js
app.locals.titulo = 'Minha API';
```

> 🔍 Usado principalmente em aplicações com **motores de template**, mas também útil para configurações compartilhadas entre arquivos e rotas.

---

### 🛤️ 9.4.2. `app.mountpath`

Indica o caminho base onde a aplicação foi "montada" como subaplicativo.

```js
console.log(app.mountpath); // "/api"
```

> ✅ Muito útil quando usamos `app.use()` para estruturar submódulos de rota ou microserviços.

---

### 🗂️ 9.4.3. `app.settings`

Armazena as configurações feitas com `app.set()`.

```js
app.set('porta', 4000);
console.log(app.settings.porta); // 4000
```

> ⚙️ Ideal para acessar e validar opções de configuração globais.

---

### 📋 9.4.4. `app._router`

Exibe a estrutura de rotas e middlewares da aplicação.

```js
console.log(app._router.stack);
```

> ⚠️ Essa é uma **propriedade interna** (por convenção, prefixo `_`), usada apenas para **debug ou documentação automatizada**.

---

### 🔁 9.4.5. `app.route(path)`

Retorna uma referência à rota para aplicar **métodos encadeados** (`GET`, `POST`, etc.).

```js
app.route('/usuarios')
   .get((req, res) => res.send('Listar usuários'))
   .post((req, res) => res.send('Criar usuário'));
```

> 📌 Útil para manter o código de múltiplos métodos HTTP mais organizado.

---

### 🧪9.4.6. `app.request` e `app.response`

Referências diretas aos objetos padrão do Express:

```js
console.log(app.request);
console.log(app.response);
```

> 🧠 Pouco utilizadas, mas interessantes em configurações avançadas de middlewares.

## ✅ Conclusão

Conhecer as **propriedades da instância `app`** ajuda a desenvolver aplicações Express mais profissionais, organizadas e fáceis de manter — além de ampliar a capacidade de debug, modularização e customização do seu backend.

---

## 🔎 9.5 – Explorando o `app.` no VSCode

Ao digitar `app.` no editor de código, o **VSCode exibe uma lista de métodos disponíveis**. Isso é possível porque o `app` é uma instância baseada na classe interna do Express.

> 💡 O VSCode oferece **IntelliSense**, que sugere métodos, mostra argumentos esperados e ajuda a evitar erros de digitação.

### Exemplos de sugestões que você verá:

- `app.use()`
- `app.get()`
- `app.route()`
- `app.listen()`
- `app.disable()`

------

## 🧠 9.6 – Boas práticas ao usar `app`

| Boa prática                                    | Por quê?                                                  |
| ---------------------------------------------- | --------------------------------------------------------- |
| Separar `server.js` e `app.js`                 | Clareza entre iniciar o servidor e configurar a aplicação |
| Aplicar middlewares com `use()` no topo        | Garante que todas as rotas herdem esses comportamentos    |
| Exportar `app` com `export default`            | Permite reutilizar em testes ou outros arquivos           |
| Centralizar rotas com `app.use('/api', rotas)` | Organização e escalabilidade do projeto                   |

------

## 🧪 9.7 – Atividade Prática

> **Objetivo**: Familiarizar-se com a instância `app` e seus métodos.

### 📌 Tarefa:

1. Crie um novo arquivo `testeApp.js`
2. Nele, importe e instancie o Express
3. Teste os seguintes comandos:

```javascript
import express from 'express';
const app = express();

app.use(express.json());
app.get('/', (req, res) => res.send('Olá, mundo!'));
app.listen(4000, () => console.log('Rodando na porta 4000'));
```

1. Execute com `node testeApp.js` e acesse [http://localhost:4000](http://localhost:4000/)
2. No terminal, digite `app.` e veja as sugestões do VSCode

------

## ⚙️ 9.8 – Recursos Avançados: `app.route()`, `app.all()` e `app.param()`

> 🧠 Nesta seção, exploramos recursos avançados da instância `app` que ajudam a criar rotas mais limpas, padronizadas e reutilizáveis.

---

## 🔁 9.8.1. `app.route()`

Permite encadear múltiplos métodos HTTP em uma **única rota**. Ideal para **organizar melhor** trechos repetitivos.

### ✅ Exemplo:

```js
app.route('/usuarios')
  .get((req, res) => res.send('Listar usuários'))
  .post((req, res) => res.send('Criar novo usuário'));
```

> 🔎 *Usado para evitar repetição de rotas como `app.get('/usuarios')`, `app.post('/usuarios')`, etc.*

---

## 🌐 9.8.2. `app.all()`

Executa a mesma função para **todos os métodos HTTP** numa rota específica. Pode ser usado como **validação ou middleware genérico**.

### ✅ Exemplo:

```js
app.all('/api/*', (req, res, next) => {
  console.log(`Método usado: ${req.method}`);
  next(); // Continua para a rota apropriada
});
```

> 🔐 *Muito útil para logs, autenticação ou filtros aplicados a várias rotas.*

---

## 🧱 9.8.3. `app.param()`

Define um **middleware que será executado sempre que um determinado parâmetro de rota for encontrado**.

### ✅ Exemplo:

```js
app.param('id', (req, res, next, id) => {
  console.log(`ID capturado: ${id}`);
  next();
});

app.get('/produtos/:id', (req, res) => {
  res.send(`Produto ${req.params.id}`);
});
```

> 💡 *Perfeito para validações de ID, busca no banco de dados, entre outros.*

---

## 🧠 Conclusão

Neste capítulo, exploramos em profundidade o **Express**, uma das bibliotecas mais poderosas e populares para criação de APIs com Node.js. Compreendemos o que é a instância `app`, como ela serve de núcleo da aplicação e como os métodos e propriedades que ela oferece nos permitem estruturar um backend moderno e escalável.

Aprendemos a utilizar:

- Os métodos fundamentais (`app.use`, `app.get`, `app.post`, etc.)
- Recursos de configuração como `app.set` e `app.listen`
- Propriedades importantes como `app.locals`, `app._router` e `app.settings`
- E até recursos mais avançados como `app.route()`, `app.all()` e `app.param()`

Também entendemos como o **VSCode pode nos ajudar com sugestões inteligentes (IntelliSense)** ao trabalhar com `app.`, e realizamos uma **atividade prática** para testar nossa aplicação localmente.

> 🎓 **Agora você tem uma base sólida sobre como o Express funciona por trás dos panos**, o que permitirá criar APIs mais organizadas, reutilizáveis e confiáveis.

---

## 📚 9.9 Referências Complementares

- [API de Referência do Express (pt-BR)](https://riptutorial.com/pt/node-js/topic/5067/express)
- [Documentação oficial do Express (EN)](https://expressjs.com/en/api.html)
- [Funções do objeto `app` no Express – Dev.to](https://dev.to/luiztools/construindo-uma-api-rest-com-nodejs-e-express-3m8h)
- [Curso Express + Node.js – YouTube (Matheus Battisti)](https://www.youtube.com/watch?v=1hpc70_OoAg)

---

## 📚 Próximo Capítulo

Agora que você entende a estrutura do Express e o papel da instância `app`, vamos aprofundar nosso conhecimento nos métodos HTTP, começando pelo `GET`.

➡️ Continue para: **[Capítulo 9.1 – Entendendo o Método HTTP GET](docs/<Capítulo 9.1 – Entendendo o Método HTTP GET.md>)**

------

⬅️ [Capítulo 08 – Rotas e Endpoints](<Capítulo 08 – Rotas e Endpoints.md>) | [🏠 Voltar à Home](<README.md>) | [Capítulo 09.1 – Entendendo o Método HTTP GET ➡️](<Capítulo 09.1 – Entendendo o Método HTTP GET.md>)
