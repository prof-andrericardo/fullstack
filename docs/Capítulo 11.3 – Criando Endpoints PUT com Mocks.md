# ✏️ Capítulo 11.3 – Criando Endpoints PUT com Mocks

> 🎯 **Objetivo**: Criar endpoints do tipo `PUT` para atualizar dados de usuários e tarefas no backend utilizando arrays mockados. Este capítulo aplica os conceitos estudados no Capítulo 11.1 de maneira prática e funcional.
>
> 👨‍🎓 Público-alvo: Alunos do 3º ano do Ensino Médio Técnico em Informática

---

## 🔧 11.3.1 – Pré-requisitos

Certifique-se de que os arquivos estão corretamente organizados:

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

## 👤 11.3.2 – Endpoint: `PUT /usuarios/:id`

Atualiza os dados de um usuário com base no `id`.

### 📌 Etapas da lógica:

1. Extrair `id` da URL
2. Verificar se o usuário existe
3. Atualizar os campos fornecidos no `body`
4. Manter o `id` original
5. Retornar o objeto atualizado com `status 200`

------

### ✅ Código:

```javascript
// Atualiza os dados de um usuário existente
router.put('/usuarios/:id', (req, res) => {
  const id = parseInt(req.params.id); // Captura o ID da URL
  const usuarioIndex = mockUsuarios.findIndex(u => u.id === id); // Procura o índice

  if (usuarioIndex === -1) {
    return res.status(404).json({
      success: false,
      error: 'Usuário não encontrado!'
    });
  }

  // Cria um novo objeto unindo os dados antigos com os novos
  const usuarioAtualizado = {
    ...mockUsuarios[usuarioIndex], // mantém os dados antigos
    ...req.body,                   // sobrescreve com os novos
    id: mockUsuarios[usuarioIndex].id // garante que o ID não mude
  };

  // Substitui o antigo pelo novo
  mockUsuarios[usuarioIndex] = usuarioAtualizado;

  // Retorna a versão atualizada
  res.status(200).json({
    success: true,
    data: usuarioAtualizado
  });
});
```

**🔍 Explicação:**

- `findIndex()` retorna a posição no array (ou -1 se não encontrar)
- `...req.body` insere os dados enviados pelo cliente
- O ID é sempre mantido
- `status(200)` retorna o usuário atualizado com sucesso

------

### 🧪 Teste com Thunder Client

- **URL**: `PUT http://localhost:3000/usuarios/2`
- **Body (JSON)**:

```json
{
  "nome": "Maria Atualizada",
  "email": "maria.novo@email.com"
}
```

- **Resposta esperada**: status `200 OK`, objeto atualizado

------

## 📋 11.3.3 – Endpoint: `PUT /tarefas/:id`

Atualiza os dados de uma tarefa. Também verifica se o `usuario_id` enviado (caso alterado) é válido.

------

### ✅ Código:

```javascript
// Atualiza uma tarefa existente
router.put('/tarefas/:id', (req, res) => {
  const id = parseInt(req.params.id);
  const tarefaIndex = mockTarefas.findIndex(t => t.id === id);

  if (tarefaIndex === -1) {
    return res.status(404).json({
      success: false,
      error: 'Tarefa não encontrada!'
    });
  }

  // Se o usuário foi alterado, valida o novo ID
  if (req.body.usuario_id) {
    const usuarioExiste = mockUsuarios.some(u => u.id === req.body.usuario_id);
    if (!usuarioExiste) {
      return res.status(404).json({
        success: false,
        error: 'Usuário não encontrado!'
      });
    }
  }

  // Atualiza os dados da tarefa
  const tarefaAtualizada = {
    ...mockTarefas[tarefaIndex],
    ...req.body,
    id: mockTarefas[tarefaIndex].id
  };

  mockTarefas[tarefaIndex] = tarefaAtualizada;

  res.status(200).json({
    success: true,
    data: tarefaAtualizada
  });
});
```

------

### 🧪 Teste com Thunder Client

- **URL**: `PUT http://localhost:3000/tarefas/1`
- **Body**:

```json
{
  "titulo": "Tarefa atualizada",
  "concluida": true,
  "usuario_id": 2
}
```

- **Resposta esperada**: status `200 OK`, tarefa atualizada com o novo usuário

------

## ⚠️ 11.3.4 – Casos de erro para testar

| Situação                           | Status esperado                                 | Mensagem de erro                 |
| ---------------------------------- | ----------------------------------------------- | -------------------------------- |
| ID não existe                      | `404`                                           | "Usuário/Tarefa não encontrada!" |
| `usuario_id` inexistente na tarefa | `404`                                           | "Usuário não encontrado!"        |
| Campos inválidos ou em branco      | `200` (sem validação de conteúdo neste estágio) |                                  |

------

## 📘 11.3.5 – Boas práticas aplicadas

| Boas práticas                         | Benefício                                      |
| ------------------------------------- | ---------------------------------------------- |
| Uso do spread operator (`...`)        | Atualização simples e legível                  |
| Preservar o `id` original             | Evita sobrescrita acidental                    |
| Validação condicional de `usuario_id` | Garante integridade da relação entre entidades |
| Resposta clara com status e JSON      | Facilita debug e integração com frontend       |

------

## 🧠 11.3.6 – Atividade Prática

> **Objetivo**: Consolidar a criação de endpoints de atualização, testando diferentes cenários e identificando erros e boas práticas.

### 📌 Desafio:

1. Atualize o nome e o e-mail de um dos usuários via Thunder Client
2. Atualize uma tarefa existente:
   - Mude o título
   - Marque como `concluída: true`
   - Atribua a outro `usuario_id` válido
3. Simule erros:
   - Tente atualizar uma tarefa com `usuario_id` inexistente
   - Tente atualizar um `id` que não existe
4. Anote os **status HTTP** e as **mensagens de resposta**

---

## 📚 11.3.7 Referências Complementares

- [Atualizando objetos com Express – YouTube (Programação Dinâmica)](https://www.youtube.com/watch?v=LUvUBqurjD4)
- [Uso avançado de spread operator em atualizações – MDN](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [Exemplo de PUT com validação de dados – Alura](https://cursos.alura.com.br/forum/topico-validacao-de-put-e-delete-156225)
- [Guia prático: Atualização em mocks para testes – Dev.to](https://dev.to/romulosilvalima/utilizando-mocks-em-testes-4j4d)

---

## 📚 Próximo Capítulo

Chegamos à etapa final do CRUD!
 Agora vamos aprender a **remover dados da API** com segurança e precisão utilizando o método `DELETE`.

➡️ Continue para: **[Capítulo 12.1 – Entendendo o Método DELETE](docs/<Capítulo 12.1 – Entendendo o Método HTTP DELETE.md>)**

------

⬅️ [Capítulo 11.2 – PUT Lógica e Organização do Pensamento](<Capítulo 11.2 – PUT Lógica e Organização do Pensamento.md>) | [🏠 Voltar à Home](<../README.md>) | [Capítulo 12.1 – Entendendo o Método HTTP DELETE ➡️](<Capítulo 12.1 – Entendendo o Método HTTP DELETE.md>)
