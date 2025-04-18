# 🧠 PUT – Lógica e Organização do Pensamento

> 🎯 **Objetivo**: Entender a lógica por trás do método HTTP `PUT`, utilizado para atualizar dados existentes em um sistema, antes de partir para a codificação.
>
> 👨‍🎓 Público-alvo: Alunos do 3º ano do Ensino Médio Técnico em Informática

---

## 🧩 1. Qual é a função de um PUT?

O método `PUT` é usado para **atualizar completamente** um recurso já existente.  
Isso significa que você envia **uma nova versão do recurso**, com os campos atualizados.

### 📚 Exemplos práticos:
- Atualizar o nome de um usuário
- Marcar uma tarefa como concluída
- Corrigir o e-mail de um cadastro

---

## 🧠 2. O que esse endpoint precisa fazer?

Vamos criar dois endpoints do tipo `PUT`:
1. Atualizar os dados de um usuário existente
2. Atualizar os dados de uma tarefa existente

---

## 🔁 3. Qual é o fluxo lógico de um PUT?

### 📝 Para `PUT /usuarios/:id`:

1. Receber o ID na URL e os dados novos no corpo (JSON)
2. Verificar se o ID existe
3. Atualizar os campos desejados
4. Manter o ID original
5. Retornar o objeto atualizado com `status 200`

---

### 📝 Para `PUT /tarefas/:id`:

1. Receber o ID e os novos dados da tarefa
2. Verificar se a tarefa existe
3. Verificar se o `usuario_id` informado ainda é válido (se for alterado)
4. Atualizar os campos informados
5. Manter o ID original
6. Retornar a nova versão da tarefa

---

## ⚙️ 4. Por que usamos `PUT`?

| Método  | Quando usar                          |
|---------|--------------------------------------|
| `PUT`   | Quando vamos **substituir/atualizar** um recurso inteiro |
| `PATCH` | Quando queremos atualizar **parcialmente** |
| `POST`  | Para criar um novo recurso           |
| `GET`   | Para buscar dados                    |
| `DELETE`| Para remover um recurso              |

---

## 📋 5. O que precisamos validar?

- Se o ID informado **existe**
- Se o novo `usuario_id` (se for alterado) é válido
- Evitar sobrescrever o ID original
- Garantir que os dados enviados no corpo sejam compatíveis com os esperados

---

## 🧠 6. Entendendo a estrutura do `app.put()`

### 📌 Sintaxe:

```js
app.put('/usuarios/:id', (req, res) => {
  const id = parseInt(req.params.id);
  const index = mockUsuarios.findIndex(u => u.id === id);

  if (index === -1) {
    return res.status(404).json({ success: false, error: 'Usuário não encontrado' });
  }

  const atualizado = {
    ...mockUsuarios[index],
    ...req.body,
    id: mockUsuarios[index].id
  };

  mockUsuarios[index] = atualizado;

  res.status(200).json({ success: true, data: atualizado });
});
```

---

### 🔍 Explicação lógica:

- **`app.put()`** → define uma rota do tipo PUT
- **`/usuarios/:id`** → o ID é passado pela URL
- **`req.params.id`** → recupera o ID da requisição
- **`findIndex()`** → procura o índice do usuário/tarefa no array
- **`...req.body`** → substitui os dados antigos pelos novos
- **`mockUsuarios[index] = atualizado`** → atualiza o valor
- **`status(200)`** → indica que foi atualizado com sucesso

---

## 📤 7. O que o sistema deve retornar?

### ✅ Em caso de sucesso:

```json
{
  "success": true,
  "data": {
    "id": 2,
    "nome": "Maria Atualizada",
    "email": "maria@nova.com"
  }
}
```

### ❌ Em caso de erro:

```json
{
  "success": false,
  "error": "Usuário não encontrado"
}
```

---

## 📚 8. Como esse endpoint se encaixa no sistema?

Toda aplicação permite ao usuário **alterar algo que já existe**.  
O `PUT` dá poder ao cliente de manter os dados atualizados e corrigir informações.  
Ele é parte essencial de qualquer sistema com formulários de edição ou atualização de status.

---

## 📝 9. Antes de codar, pense:

1. Qual item desejo atualizar?
2. O ID foi enviado corretamente?
3. O que pode ou não ser alterado?
4. Preciso validar o que?
5. Como devo tratar se o item não existir?
6. E o que devolvo se der certo?

> 🧠 Pensar antes de codar evita bugs e aumenta a confiança no seu código!

---
