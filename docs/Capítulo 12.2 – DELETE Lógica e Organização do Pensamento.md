# 🧠 DELETE – Lógica e Organização do Pensamento

> 🎯 **Objetivo**: Compreender a lógica por trás do método HTTP `DELETE`, utilizado para remover dados de um sistema. Foco no raciocínio antes da codificação.
>
> 👨‍🎓 Público-alvo: Alunos do 3º ano do Ensino Médio Técnico em Informática

---

## 🧩 12.2.1 Qual é a função de um DELETE?

O método `DELETE` é usado para **remover definitivamente** um item de um sistema.  
Esse tipo de requisição apaga um dado existente, baseado no ID.

### 📚 Exemplos práticos:
- Apagar um usuário do sistema
- Deletar uma tarefa finalizada
- Remover um produto descontinuado

---

## 🧠 12.2.2 O que esse endpoint precisa fazer?

Vamos criar dois endpoints do tipo `DELETE`:
1. Remover um usuário pelo seu ID
2. Remover uma tarefa específica pelo ID

---

## 🔁 12.2.3 Qual é o fluxo lógico de um DELETE?

### 📝 Para `DELETE /usuarios/:id`:

1. Receber o ID do usuário na URL
2. Verificar se esse ID existe no sistema
3. Se não existir, retornar erro `404`
4. Se existir, remover o usuário do array
5. Retornar `status 204` (sem conteúdo)

---

### 📝 Para `DELETE /tarefas/:id`:

1. Receber o ID da tarefa na URL
2. Verificar se a tarefa existe
3. Se não existir, retornar erro `404`
4. Se existir, remover a tarefa do array
5. Retornar `status 204`

---

## ⚙️ 12.2.4 Por que usamos `DELETE`?

| Método   | Quando usar                          |
|----------|--------------------------------------|
| `DELETE` | Quando precisamos **remover** algo permanentemente |
| `PUT`    | Para atualizar dados existentes      |
| `POST`   | Para criar novos registros           |
| `GET`    | Para buscar dados                    |

---

## 📋 12.2.5 O que precisamos validar?

- Se o ID informado **existe**
- Garantir que não estamos tentando excluir algo inexistente
- Usar status `204` corretamente (resposta sem corpo)

---

## 🧠 12.2.6 Entendendo a estrutura do `app.delete()`

### 📌 Sintaxe:

```js
app.delete('/usuarios/:id', (req, res) => {
  const id = parseInt(req.params.id);
  const index = mockUsuarios.findIndex(u => u.id === id);

  if (index === -1) {
    return res.status(404).json({ success: false, error: 'Usuário não encontrado' });
  }

  mockUsuarios.splice(index, 1);

  res.status(204).end(); // Sem corpo na resposta
});
```

---

### 🔍 Explicação lógica:

- **`app.delete()`** → define uma rota para deletar um item
- **`/usuarios/:id`** → o ID do item a ser removido vem na URL
- **`findIndex()`** → retorna o índice do item no array (ou -1 se não encontrar)
- **`splice()`** → remove o item do array
- **`res.status(204).end()`** → resposta de sucesso sem conteúdo (padrão do DELETE)

---

## 📤 12.2.7 O que o sistema deve retornar?

### ✅ Em caso de sucesso:

- Apenas o status `204`  
- **Nenhum conteúdo no corpo da resposta**

### ❌ Em caso de erro:

```json
{
  "success": false,
  "error": "Tarefa não encontrada"
}
```

---

## 📚 12.2.8 Como esse endpoint se encaixa no sistema?

A exclusão é fundamental para manter os dados do sistema **limpos e atualizados**.  
O `DELETE` permite que o usuário **gerencie seu conteúdo** e remova o que não é mais necessário.

---

## 📝 12.2.9 Antes de codar, pense:

1. Qual item será removido?
2. Como ele será identificado?
3. O que acontece se o ID não existir?
4. A resposta terá conteúdo?
5. Que status deve ser usado?

> 🧠 A lógica vem antes da tecla ENTER.

---

---

## 📚 12.2.10 Referências Complementares

- [Planejamento lógico para exclusões seguras – Alura](https://cursos.alura.com.br/forum/topico-planejamento-para-deletes-125121)
- [Boas práticas em exclusão lógica e física – Dev.to](https://dev.to/andrebnassi/remocao-fisica-vs-remocao-logica-em-apis-rest-47pp)
- [findIndex e splice explicados – MDN](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
- [Exclusão de itens com mocks – YouTube (Programação Dinâmica)](https://www.youtube.com/watch?v=LUvUBqurjD4)

---

⬅️ [Capítulo 12.1 – Entendendo o Método HTTP DELETE](<Capítulo 12.1 – Entendendo o Método HTTP DELETE.md>) | [🏠 Voltar à Home](<README.md>) | [Capítulo 12.3 – Criando Endpoints DELETE com Mocks ➡️](<Capítulo 12.3 – Criando Endpoints DELETE com Mocks.md>)
