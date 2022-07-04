<script>
import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    return {
      livros: [
        {
          id: "8ae6623d-5462-4774-b5e1-e263c5d2d367",
          nome: "Livro 1",
          isbn: "978-3-16-148410-0",
          quantidade: "1",
          preco: "29,99",
        },
      ],
      novo_livro: "",
      novo_isbn: "",
      nova_qntd: "",
      novo_preco: "",
    };
  },

  methods: {
    salvar() {
      if (this.novo_livro !== "") {
        const novo_id = uuidv4();
        this.livros.push({
          id: novo_id,
          nome: this.novo_livro,
          isbn: this.novo_isbn,
          quantidade: this.nova_qntd,
          preco: this.novo_preco,
        });
        (this.novo_livro = ""),
          (this.novo_isbn = ""),
          (this.nova_qntd = ""),
          (this.novo_preco = "");
      }
    },
    excluir(livros) {
      const indice = this.livros.indexOf(livros);
      this.livros.splice(indice, 1);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Gerenciamento de Livros</h2>
    </div>
    <div class="form-input">
      <input type="text" v-model="novo_livro" placeholder="título..." />
      <input type="text" v-model="novo_isbn" placeholder="isbn..." />
      <input type="number" v-model="nova_qntd" placeholder="quantidade..." />
      <input type="text" v-model="novo_preco" placeholder="preço..." />
      <button @click="salvar">Adicionar</button>
    </div>
    <div class="list-livros">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Título</th>
            <th>ISBN</th>
            <th>Quantidade</th>
            <th>Preço</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="livros in livros" :key="livros.id">
            <td>{{ livros.id }}</td>
            <td>{{ livros.nome }}</td>
            <td>{{ livros.isbn }}</td>
            <td>{{ livros.quantidade }}</td>
            <th>{{ livros.preco }}</th>
            <td>
              <button class="delete" @click="excluir(livros)">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style>
.delete {
  background-color: #14213d;
  color: #fca311;
  border: #fca311;
  border-radius: 20px;
  width: 50%;
  height: 30px;
}
.title {
  margin-top: 2rem;
  display: flex;
  justify-content: center;
}
.form-input {
  margin-top: 10px;
  display: flex;
  justify-content: center;
}

.form-input input {
  width: 20%;
  height: 40px;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 0 10px;
}

.form-input button {
  margin-left: 1%;
  width: 10%;
  height: 40px;
  border: 1px solid rgb(36, 127, 65);
  border-radius: 10px;
  background-color: rgb(36, 127, 65);
  color: white;
  font-weight: bold;
  cursor: pointer;
}

.list-livros {
  display: flex;
  justify-content: center;
}

table {
  width: 100%;
  margin: 2% auto;
  border-collapse: collapse;
}

table tr th {
  border: 1px solid #ccc;
  padding: 20px;
  font-weight: bold;
}

table tr td {
  border: 1px solid #ccc;
  padding: 10px;
}

table tr:nth-child(odd) {
  background-color: #ccc;
}
</style>
