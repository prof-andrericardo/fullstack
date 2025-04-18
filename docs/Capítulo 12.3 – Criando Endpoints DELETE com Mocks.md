# 🧹 Capítulo 12.2 – Criando Endpoints DELETE com Mocks

> 🎯 **Objetivo**: Implementar endpoints `DELETE` para remover usuários e tarefas de arrays simulados (mocks), aplicando validações adequadas e retornando os status HTTP corretos.
>
> 👨‍🎓 Público-alvo: Alunos do 3º ano do Ensino Médio Técnico em Informática

---

## 📦 12.2.1 – Organização inicial

Certifique-se de que os seguintes arquivos estão configurados:

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

## 👤 12.2.2 – Endpoint: `DELETE /usuarios/:id`

O método `DELETE` é usado para **excluir permanentemente** um registro identificado por `ID`.

### ✅ Código:

```javascript
// Rota que remove um usuário pelo ID
router.delete('/usuarios/:id', (req, res) => {
  const id = parseInt(req.params.id); // Captura o ID da URL
  const index = mockUsuarios.findIndex(u => u.id === id); // Encontra o índice no array

  if (index === -1) {
    // Se não encontrar, responde com erro
    return res.status(404).json({
      success: false,
      error: 'Usuário não encontrado!'
    });
  }

  // Remove o usuário do array com base no índice
  mockUsuarios.splice(index, 1);

  // Retorna status 204 (sem conteúdo)
  res.status(204).end();
});
```

**🔍 Explicação:**

- `findIndex()` localiza o índice no array
- `splice()` remove o item do array com base na posição
- `status(204)` indica sucesso na exclusão **sem retornar conteúdo**

------

### 🧪 Teste com Thunder Client

- **URL**: `DELETE http://localhost:3000/usuarios/2`
- **Esperado**:
  - Status: `204 No Content`
  - Corpo: *nenhum*
- **Teste de erro**:
  - Repetir a requisição no mesmo ID
  - Status esperado: `404`

------

## 📋 12.2.3 – Endpoint: `DELETE /tarefas/:id`

Remove uma tarefa específica, caso exista.

### ✅ Código:

```javascript
// Rota que remove uma tarefa pelo ID
router.delete('/tarefas/:id', (req, res) => {
  const id = parseInt(req.params.id);
  const index = mockTarefas.findIndex(t => t.id === id);

  if (index === -1) {
    return res.status(404).json({
      success: false,
      error: 'Tarefa não encontrada!'
    });
  }

  mockTarefas.splice(index, 1);

  res.status(204).end();
});
```

**🔍 Explicação:**

- Processo idêntico ao anterior, mas aplicado ao array de tarefas
- Reforça o uso correto do `204 No Content` para deletar com sucesso

------

### 🧪 Teste com Thunder Client

- **URL**: `DELETE http://localhost:3000/tarefas/1`
- **Status esperado**: `204`
- **Erro esperado**: tentar deletar o mesmo ID novamente → status `404`

------

## ✅ 12.2.4 – Boas práticas aplicadas

| Prática                        | Explicação                                            |
| ------------------------------ | ----------------------------------------------------- |
| Verificar existência do item   | Evita apagar registros inexistentes (retorna `404`)   |
| Usar `splice()` com índice     | Remove o item com precisão do array mock              |
| Retornar status `204`          | Segue o padrão REST de sucesso na exclusão            |
| Não retornar corpo na resposta | Padrão recomendado pelo protocolo HTTP (`No Content`) |

------

## ⚠️ 12.2.5 – Erros comuns ao usar DELETE

| Erro                                  | Causa                                 | Correção                           |
| ------------------------------------- | ------------------------------------- | ---------------------------------- |
| `undefined` ao remover                | Usou `find()` em vez de `findIndex()` | Usar o índice com `splice()`       |
| Corpo de resposta retornado com `204` | Não necessário                        | Use apenas `res.status(204).end()` |
| Apagar algo já removido               | ID não é mais encontrado              | Retornar `404 Not Found`           |

------

## 🧠 12.2.6 – Atividade Prática

> **Objetivo**: Consolidar o uso do método `DELETE` testando diferentes cenários e validando os comportamentos da API.

### 📌 Desafio:

1. Crie um novo usuário e uma nova tarefa usando `POST`
2. Confirme que eles foram criados com sucesso (`GET`)
3. Apague o usuário e a tarefa criados (`DELETE`)
4. Tente apagar novamente → verifique o retorno `404`
5. Registre os seguintes dados:
   - Status HTTP de cada operação
   - Se houve ou não corpo na resposta
   - O que aconteceu no array (via `console.log()` no backend, se quiser)

------

## 📚 12.2.7 – Encerramento do CRUD com Mock

Parabéns! Agora você domina **todos os quatro métodos do CRUD** em uma API REST utilizando mocks como fonte de dados:

| Método   | Função      |
| -------- | ----------- |
| `GET`    | Ler dados   |
| `POST`   | Criar dados |
| `PUT`    | Atualizar   |
| `DELETE` | Remover     |

------

## 📘 12.2.8 – Próximo Capítulo

Agora que o CRUD foi finalizado com sucesso usando mocks, no próximo capítulo iniciaremos a conexão da API com o banco de dados MySQL, substituindo os dados simulados por dados reais.

➡️ Continue para: **[Capítulo 13 – Conectando ao MySQL com `mysql2`](https://chatgpt.com/g/g-p-67e5b2a26c7c81918301ede108f78b6a-backend-nodejs/c/cap13-mysql-conexao.md)**

------

