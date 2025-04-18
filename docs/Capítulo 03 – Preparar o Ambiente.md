# 🔧 Capítulo 3 – Preparar o Ambiente

> 🎯 **Objetivo**: Neste capítulo, você vai configurar o ambiente de desenvolvimento para a criação de uma API RESTful utilizando Node.js e as bibliotecas essenciais: **Express**, **MySQL2**, **CORS**, **DOTENV** e **Nodemon**.  
> 🧑‍🎓 **Público-alvo**: Alunos do 3º ano do Ensino Médio Técnico em Informática.

---

## 📦 3.1 – Inicializando o Projeto com `npm`

1. Abra o terminal integrado no VSCode (`Ctrl + '` ou `Ctrl + J`)
2. Navegue até a pasta `backend/`
3. Execute o comando:

```bash
npm init -y
```

> ✅ Isso criará automaticamente o arquivo `package.json` com configurações básicas padrão.

------

## 📝 3.2 – Editando o `package.json`

Substitua o conteúdo do `package.json` com a seguinte configuração personalizada:

```json
{
  "name": "todo-list-api",
  "version": "1.0.0",
  "description": "API para gerenciamento de lista de tarefas",
  "main": "server.js",
  "type": "module",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "author": "Seu Nome",
  "license": "ISC"
}
```

### 🎯 Sobre os Scripts:

| Script  | Comando             | Finalidade                                         |
| ------- | ------------------- | -------------------------------------------------- |
| `start` | `node server.js`    | Executa a aplicação em ambiente de produção        |
| `dev`   | `nodemon server.js` | Reinicia automaticamente durante o desenvolvimento |

> ⚠️ **Atenção**: o campo `"type": "module"` é essencial para utilizar a sintaxe `import/export`.

------

## 📚 3.3 – Instalando as Dependências

No Node.js, utilizamos o comando `npm install` para instalar bibliotecas externas (também chamadas de **dependências**).  
Essas bibliotecas podem ser classificadas em dois tipos:

---

### 📦 Tipos de Dependências no Projeto

| Tipo                                               | Uso principal                                                |
| -------------------------------------------------- | ------------------------------------------------------------ |
| **Dependências de Produção** (`--save`)            | São utilizadas **durante a execução** do sistema (ex: Express) |
| **Dependências de Desenvolvimento** (`--save-dev`) | São usadas **somente durante o desenvolvimento**, testes ou build (ex: Nodemon) |

> ⚠️ Em versões mais recentes do npm (`npm 5+`), o `--save` é **implícito**, ou seja, não precisa ser digitado — mas usamos aqui por fins didáticos e clareza.

---

### ▶️ Dependências de Produção

```bash
npm install --save express mysql2 cors dotenv
```

| Pacote    | Função no Projeto                                            |
| --------- | ------------------------------------------------------------ |
| `express` | Framework que gerencia rotas e requisições/respostas da API  |
| `mysql2`  | Driver para conectar o Node.js ao banco de dados MySQL       |
| `cors`    | Middleware que permite que o frontend acesse a API           |
| `dotenv`  | Permite usar variáveis de ambiente (como senhas) com segurança |

------

### 🛠️ Dependência de Desenvolvimento

```bash
npm install --save-dev nodemon morgan

```

| Pacote    | Função                                                       |
| --------- | ------------------------------------------------------------ |
| `nodemon` | Reinicia automaticamente o servidor ao detectar alterações nos arquivos |
| `morgan`  | Gera logs detalhados das requisições no terminal durante o desenvolvimento |

> ✅ Ao instalar com `--save-dev`, o pacote **não será instalado** em ambientes de produção (ex: quando o projeto for publicado no servidor).
>
> 💡 O uso do `morgan` facilita o rastreamento de problemas durante os testes da API, mostrando o método, a rota, o tempo de resposta e o status da requisição no terminal.

------

### ✅ Verificação da Instalação

Após a instalação, você pode verificar os pacotes com:

```bash
npm list --depth=0
```

Saída esperada:

```
├── cors@2.8.5
├── dotenv@16.5.0
├── express@4.18.2
├── mysql2@3.6.0
├── morgan@1.10.0
└── nodemon@3.0.2 (dev)
```

> 🎯 Os pacotes com `(dev)` são **dependências de desenvolvimento**.

------

## 🔐 3.4 – Configuração de Segurança com `.env` e `.gitignore`

### 📁 Criando o `.gitignore`

Crie um arquivo chamado `.gitignore` na raiz do projeto (`backend/`) com o seguinte conteúdo:

```bash
node_modules/
.env
```

> 🎯 Isso impede que a pasta `node_modules` e o arquivo `.env` sejam enviados para o GitHub (protegendo dados sensíveis).

------

### 📝 Criando o Arquivo `.env`

Crie o arquivo `.env` na raiz do projeto e adicione:

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=senhaSegura123
DB_NAME=todo_list_db
PORT=3000
```

| Variável      | Significado                                  |
| ------------- | -------------------------------------------- |
| `DB_HOST`     | Endereço do banco de dados (localhost/local) |
| `DB_USER`     | Nome do usuário do banco (ex: root)          |
| `DB_PASSWORD` | Senha do banco de dados                      |
| `DB_NAME`     | Nome do banco que será usado na aplicação    |
| `PORT`        | Porta onde o servidor Node.js vai rodar      |

> 💡 Essas variáveis serão acessadas com `process.env.NOME_DA_VARIAVEL`.

------

## 🛡️ 3.5 – Diferença entre `dependencies` e `devDependencies`

| Tipo              | Quando são usadas                | Exemplos                    |
| ----------------- | -------------------------------- | --------------------------- |
| `dependencies`    | Durante a execução da aplicação  | `express`, `mysql2`, `cors` |
| `devDependencies` | Apenas durante o desenvolvimento | `nodemon`, `eslint`, `jest` |

------

A seguir, trago a **versão revisada e enriquecida da seção**, com esse novo conteúdo integrado, mantendo o estilo didático e o padrão visual da documentação:

------

## 📘 3.6 – Estrutura Final do `package.json`

Após todas as configurações, o seu arquivo `package.json` ficará com a seguinte estrutura:

```json
{
  "name": "todo-list-api",
  "version": "1.0.0",
  "description": "API para gerenciamento de lista de tarefas",
  "main": "server.js",
  "type": "module",
  "scripts": {
    "start": "node server.js",
    "dev": "nodemon server.js"
  },
  "dependencies": {
    "cors": "^2.8.5",
    "dotenv": "^16.5.0",
    "express": "^4.18.2",
    "mysql2": "^3.6.0"
  },
  "devDependencies": {
    "morgan": "^1.10.0",
    "nodemon": "^3.0.2"
  }
}
```

------

### 🧠 Entendendo a importância do `package.json`

O `package.json` é o **coração do projeto Node.js**. Ele contém:

- 📛 Informações sobre o projeto (nome, versão, descrição)
- 📦 Lista de dependências instaladas
- 🏁 Scripts que ajudam a executar comandos de forma simplificada
- ⚙️ Configurações específicas, como `type: "module"` para usar `import/export`

> 📂 **É como um "RG" do seu projeto.**

------

### 🔄 Reaproveitamento em outros projetos

Uma das grandes vantagens desse arquivo é que ele pode ser **reutilizado como base para outros projetos semelhantes**, poupando tempo e evitando erros.

> 💡 **Se você guardar esse `package.json`, poderá iniciar um novo projeto com as mesmas dependências** executando apenas:

```bash
npm install
```

Esse comando irá:

- Ler o `package.json`
- Instalar automaticamente todos os pacotes listados nas seções `dependencies` e `devDependencies`
- Criar a pasta `node_modules/` e o arquivo `package-lock.json`

------

### 🎯 Dica profissional

> “Sempre que finalizar a configuração de um projeto bem estruturado, salve uma cópia do `package.json`. Ele pode ser o ponto de partida de futuros projetos com uma arquitetura semelhante.”

---

## 🧪 3.7 – Testando a Estrutura do Projeto

1. Execute no terminal:

```bash
npm run dev
```

1. Verifique a saída:

```
[nodemon] starting `node server.js`
✅ Servidor rodando na porta 3000
```

> ❌ Se aparecer erro `SyntaxError: Cannot use import statement`, verifique se `"type": "module"` está no `package.json`.

------

## ⚠️ 3.8 – Erros Comuns e Soluções

| Erro                                       | Causa Provável                               | Solução                                        |
| ------------------------------------------ | -------------------------------------------- | ---------------------------------------------- |
| `SyntaxError: Cannot use import statement` | `"type": "module"` ausente no `package.json` | Adicione `"type": "module"`                    |
| `Error [ERR_MODULE_NOT_FOUND]`             | Importação com caminho errado                | Verifique e inclua extensão `.js` nos `import` |
| `PORT já está em uso`                      | Porta 3000 ocupada                           | Altere para 3001, 4000 ou outra disponível     |
| `.env não está sendo lido`                 | `dotenv` não foi carregado                   | Importe `dotenv.config()` no `conexaoSQL.js`   |

------

## 🧠 3.9 – Atividade Prática: Criar sua API “Alunos”

> ✏️ **Objetivo**: Reforçar os conceitos estudados criando um ambiente similar para uma nova API.

### 📌 Desafio:

Crie um projeto chamado `api-alunos` e configure seu ambiente seguindo os passos abaixo:

1. Crie a pasta `api-alunos/backend`

2. Execute `npm init -y`

3. Configure o `package.json` com `type: "module"` e scripts `start` e `dev`

4. Instale:

   ```bash
   npm install --save express mysql2 cors dotenv
   npm install --save-dev nodemon
   ```

5. Crie `.env` e `.gitignore`

6. Rode `npm run dev` e valide a estrutura

> 💡 **Dica bônus**: já inclua uma rota de teste no `server.js` para retornar um `Olá, mundo!`.

------

## 📚 3.10 – Próximo Capítulo

➡️ No próximo capítulo, vamos **iniciar o servidor e configurar o Express no `server.js`**.

Continue para: **[Capítulo 4 – Configurar o Express](Capítulo 4 – Configurar o Express.md)**

------

