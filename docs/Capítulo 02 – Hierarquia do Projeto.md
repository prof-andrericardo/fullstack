# 📁 Capítulo 2 – Hierarquia do Projeto

> 🔧 **Objetivo**: Neste capítulo, vamos estruturar o projeto Backend com Node.js, organizando as pastas e arquivos necessários para o desenvolvimento de uma API RESTful.  
> ✏️ **Nível**: Iniciante – voltado para alunos do 3º ano do Técnico em Informática.

---

## 🚀 2.1 – Pré-requisitos

Antes de começar, abra o terminal e verifique se você tem as versões mínimas do Node.js e do npm instaladas:

```bash
node --version  # v16 ou superior
npm --version   # v8 ou superior
```

> 💡 Caso alguma versão esteja desatualizada, consulte o professor ou atualize via [site oficial do Node.js](https://nodejs.org/).

------

## 🧱 2.2 – Estrutura de Diretórios e Arquivos

### 📂 Passo 1 – Criar a Pasta do Projeto no VSCode

1. Abra o **VSCode**
2. Vá em `File > Open Folder` e crie uma pasta chamada `projeto`
3. Dentro dela, crie uma subpasta chamada `backend`
4. Agora abra a pasta `backend/` no VSCode

------

### 📂 Passo 2 – Criar a Estrutura de Arquivos

Abra o terminal integrado no VSCode (atalho: `Ctrl + '` ou `Ctrl + J`) e digite:

```bash
# Criar as pastas principais
mkdir -p src/{routes,mocks} utils

# Criar os arquivos essenciais
touch package.json server.js src/app.js src/conexaoSQL.js src/routes/api.js src/mocks/mockTarefas.js utils/funcoes-auxiliares.js
```

------

### 🗂️ Estrutura Final Esperada

```plaintext
backend/
├── package.json
├── server.js
├── src/
│   ├── app.js
│   ├── conexaoSQL.js
│   ├── routes/
│   │   └── api.js
│   └── mocks/
│       └── mockTarefas.js
└── utils/
    └── funcoes-auxiliares.js
```

------

## 🧠 2.3 – Entendendo a Estrutura

### 📦 Arquivos da Raiz

| Arquivo        | Função                                                       |
| -------------- | ------------------------------------------------------------ |
| `package.json` | Gerencia dependências e scripts (`start`, `dev`) do projeto  |
| `server.js`    | Inicia o servidor Express e integra com `app.js` e as rotas da aplicação |

------

### 📂 Diretório `src/`

| Arquivo/Pasta          | Função                                                       |
| ---------------------- | ------------------------------------------------------------ |
| `app.js`               | Configura o Express com os middlewares globais (JSON, CORS, logs) |
| `conexaoSQL.js`        | Concentra a configuração para conectar com o banco de dados MySQL |
| `routes/api.js`        | Define os endpoints da API (usuários, tarefas)               |
| `mocks/mockTarefas.js` | Contém dados fictícios para testes antes do MySQL real       |

------

### 🛠️ Diretório `utils/`

| Arquivo                 | Função                                                       |
| ----------------------- | ------------------------------------------------------------ |
| `funcoes-auxiliares.js` | Armazena funções genéricas reutilizáveis como `formatarData()` |

------

## 💡 2.4 – Por que separar pastas e arquivos?

Essa organização segue o princípio da **Separação de Responsabilidades (SoC – Separation of Concerns)**, muito utilizado no mercado de software. Cada parte do projeto tem uma função específica, o que traz os seguintes benefícios:

- ✅ **Facilita a leitura e manutenção do código**
- 🧩 **Permite dividir tarefas entre membros da equipe**
- 🔍 **Ajuda a encontrar erros e testar partes isoladas**
- 🔄 **Facilita atualizações sem quebrar todo o sistema**

------

## 🧪 2.5 – Exemplo de Conteúdo (mockTarefas.js)

```javascript
// src/mocks/mockTarefas.js
export default [
  {
    id: 1,
    titulo: "Estudar Node.js",
    descricao: "Praticar middlewares",
    concluida: false,
    criado_em: "2023-10-25",
    usuario_id: 1
  },
  {
    id: 2,
    titulo: "Comprar ingredientes",
    descricao: "Leite, ovos, pão",
    concluida: true,
    criado_em: "2023-10-24",
    usuario_id: 2
  }
];
```

------

## 💼 2.6 – Boas Práticas

### 🧠 Nomenclatura Inteligente

> Use nomes autoexplicativos e prefixos que indiquem o papel dos arquivos:

| Nome sugerido           | Função                                           |
| ----------------------- | ------------------------------------------------ |
| `tarefas.routes.js`     | Define as rotas de tarefas                       |
| `tarefas.controller.js` | Controla a lógica das tarefas                    |
| `tarefas.model.js`      | (opcional, se usar banco) Define consultas ao BD |

------

### ⚙️ Atalhos do VSCode que Ajudam Muito

| Atalho             | Função                              |
| ------------------ | ----------------------------------- |
| `Ctrl + P`         | Buscar arquivos rapidamente         |
| `Ctrl + Shift + F` | Buscar por palavras no projeto todo |

------

### 🧩 Extensões Recomendadas

| Nome da Extensão | Descrição                                       |
| ---------------- | ----------------------------------------------- |
| MySQL2           | Visualização e conexão com o banco de dados     |
| Thunder Client   | Testes de API direto no VSCode                  |
| REST Client      | Alternativa para requisições sem sair do VSCode |

------

## 🔍 2.7 – Verificação Final

✅ Ao final deste capítulo, verifique se:

- A estrutura de pastas e arquivos está correta
- Os arquivos estão vazios ou com comentários tipo `// TODO`
- Você entende a função de cada parte do projeto

------

## 🧠 2.8 – Reflexão Final

> “A organização do projeto é o primeiro passo para um software de qualidade. Bons hábitos de hoje evitam problemas amanhã.”

------

## 🧪 2.9 – Desafio Prático

> 💡 **Crie um projeto semelhante para um sistema de cadastro de produtos.**
>
> Estrutura recomendada:

```plaintext
backend/
├── src/
│   ├── routes/
│   │   └── produtos.routes.js
│   └── mocks/
│       └── mockProdutos.js
└── utils/
    └── funcoes-produto.js
```

**Sua tarefa:**

1. Crie a estrutura acima
2. Adicione ao menos um produto no `mockProdutos.js`

---

## 📚 2.10 Referências Complementares

- [Boas práticas de organização de projetos Node.js – Rockseat](https://blog.rocketseat.com.br/estrutura-de-pastas-para-projetos-nodejs/)
- [Como organizar a estrutura de uma API REST – Medium/Thiago Marinho](https://medium.com/@thiagolnr/como-organizar-uma-api-rest-com-node-js-8c00f7ef55a)
- [Organizando projetos backend em camadas – Alura](https://www.alura.com.br/artigos/estrutura-backend-projeto-node)
- [Padrões de arquitetura para APIs RESTful – DevMedia](https://www.devmedia.com.br/padroes-de-projeto-para-api-rest/37699)

------

## 📚 Próximo Capítulo

➡️ Vamos preparar o ambiente e instalar as dependências da API.
 Continue para: **[Capítulo 3 – Preparar o Ambiente](docs/<Capítulo 3 – Preparar o Ambiente.md>)**

------

⬅️ [Capítulo 01 – Introdução ao Projeto e à API RESTful](<Capítulo 01 – Introdução ao Projeto e à API RESTful.md>) | [🏠 Voltar à Home](<../README.md>) | [Capítulo 03 – Preparar o Ambiente ➡️](<Capítulo 03 – Preparar o Ambiente.md>)
