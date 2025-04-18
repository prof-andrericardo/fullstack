# 📘 Capítulo 01 – Introdução ao Projeto e à API RESTful

> 🎯 **Objetivo deste capítulo:**  
> Apresentar de forma clara, motivadora e acessível o que é uma API, como funciona uma API RESTful, e o que será desenvolvido ao longo do tutorial completo. Ideal para alunos do Ensino Médio Técnico em Informática que estão tendo seu primeiro contato com backend.

---

## 🔍 1.1 O que é uma API?

**API** significa **Interface de Programação de Aplicações** (do inglês *Application Programming Interface*).  
Na prática, é um **meio de comunicação entre dois sistemas**, como um aplicativo e um servidor.

### 📱 Exemplos reais de uso de APIs:

| Ação que você faz           | API que está por trás                                  |
|-----------------------------|---------------------------------------------------------|
| Abrir o clima no celular    | A API do clima envia dados do tempo                     |
| Fazer login no Instagram    | A API do Instagram autentica o seu usuário              |
| Buscar um produto na Shopee | A API da Shopee retorna os produtos da pesquisa         |
| Enviar uma mensagem no WhatsApp Web | A API envia seu texto ao servidor e ao destinatário   |

---

## 🔄 1.2 O que é uma API RESTful?

Uma **API RESTful** segue um conjunto de regras chamado **REST (Representational State Transfer)**.

### ✅ Características de uma API RESTful:

- Usa o protocolo **HTTP**
- Trabalha com **métodos** como `GET`, `POST`, `PUT` e `DELETE`
- Manipula **recursos** (ex: usuários, tarefas, produtos)
- Cada recurso tem sua **URL própria**
- Responde sempre com **status HTTP** e geralmente com **JSON**

---

### 🧭 Exemplo prático:

Imagine uma API de usuários com a seguinte rota:

```htaccess
GET /usuarios
```

O que acontece:

- O **cliente** (navegador, app, Thunder Client) envia uma requisição
- O **servidor** responde com os dados dos usuários em formato JSON

```json
{
  "success": true,
  "data": [
    { "id": 1, "nome": "Lucas" },
    { "id": 2, "nome": "Ana" }
  ]
}
```

---

## 🧰 1.3 O que vamos construir neste projeto?

Você vai desenvolver uma API RESTful completa para gerenciar uma **lista de tarefas (To-Do List)**.  
Ela será capaz de:

- ✅ Cadastrar usuários e tarefas
- 🔍 Consultar tarefas por ID ou nome
- ✏️ Atualizar informações
- 🗑️ Remover registros
- 🧪 Ser testada com o Thunder Client
- 🛢️ Posteriormente, será conectada a um banco de dados MySQL

---

## 🧱 1.4 Tecnologias utilizadas

| Tecnologia     | Finalidade                                               |
|----------------|-----------------------------------------------------------|
| **Node.js**    | Ambiente para rodar JavaScript no backend                |
| **Express**    | Framework para criar rotas e lidar com requisições       |
| **Nodemon**    | Reinicia o servidor automaticamente durante o dev        |
| **dotenv**     | Gerencia variáveis de ambiente com segurança             |
| **MySQL2**     | Driver para conectar com banco de dados                  |
| **Thunder Client** | Ferramenta para testar APIs dentro do VS Code      |

---

## 🧭 1.5 Organização do curso

O projeto está dividido em **capítulos numerados**, cada um focando em:

1. 📘 Conceito (entendimento teórico)
2. 🧠 Lógica (planejamento do que será feito)
3. 💻 Código (implementação prática com explicações comentadas)

Exemplo de sequência:

- Capítulo 09.1 – Entendendo o Método `GET`
- Capítulo 09.2 – GET: Lógica e Organização do Pensamento
- Capítulo 09.3 – Criando Endpoints `GET` com Mocks

---

## 👨‍🎓 1.6 Perfil e pré-requisitos

Este tutorial foi desenvolvido para alunos que:

- Estão cursando o **Ensino Médio Técnico em Informática**
- Já possuem noções básicas de **JavaScript**
- Desejam aprender **desenvolvimento backend**
- Estão iniciando com **APIs e bancos de dados**

Não é necessário ter experiência com Node.js ou Express.  
Todos os passos são detalhados e acompanhados de explicações acessíveis.

---

## 📚 1.7 Mini glossário introdutório

| Termo            | Significado                                                        |
|------------------|--------------------------------------------------------------------|
| **API**          | Interface de comunicação entre sistemas                           |
| **Endpoint**     | Um "ponto de acesso" da API (ex: `GET /usuarios`)                 |
| **Cliente**      | Quem faz a requisição (navegador, app, sistema externo)            |
| **Servidor**     | Quem processa e responde às requisições                           |
| **Requisição**   | Pedido enviado pelo cliente (`req`)                                |
| **Resposta**     | Retorno enviado pelo servidor (`res`)                              |
| **JSON**         | Formato leve de dados usado para enviar/receber informações        |
| **Mock**         | Simulação de dados reais, usados para testes                       |

---

## 💬 1.8 Por que aprender Backend com Node.js?

- Porque JavaScript já é conhecido pela maioria dos alunos
- Porque Node.js é moderno, leve e usado no mercado
- Porque APIs são a base da web moderna
- Porque permite criar **sistemas reais com lógica de verdade**

---

## 📚 1.9 Referências Complementares

- [O que é uma API – Programação Dinâmica (YouTube)](https://www.youtube.com/watch?v=vGuqKIRWosk)
- [Entendendo REST – Curso em Vídeo](https://www.youtube.com/watch?v=ghTrp1x_1As)
- [Documentação oficial do Node.js (pt-BR)](https://nodejs.org/pt-br/docs/)
- [Documentação oficial do Express (traduzido)](https://riptutorial.com/pt/node-js)
- [Artigo: Diferença entre API, REST e RESTful – DevMedia](https://www.devmedia.com.br/entendendo-as-diferencas-entre-api-rest-e-restful/37684)
- [Guia rápido de HTTP para iniciantes – Alura](https://www.alura.com.br/artigos/o-que-e-o-protocolo-http)

---

## 🚀 Vamos começar?

A partir do Capítulo 2, iniciaremos a estruturação do projeto passo a passo.  
Você poderá:

- Rodar um servidor local
- Criar seus próprios endpoints
- Testar com Thunder Client
- E futuramente integrar com MySQL

> 👨‍💻 Este tutorial vai transformar você em um desenvolvedor backend iniciante com base sólida.

---

⬅️ [ ]() | [🏠 Voltar à Home](<../README.md>) | [Capítulo 02 – Hierarquia do Projeto ➡️](<Capítulo 02 – Hierarquia do Projeto.md>)
