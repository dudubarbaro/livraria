<script>
import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    return {
      categorias: [
        { id: "8ae6623d-5462-4774-b5e1-e263c5d2d367", nome: "Gênero A" },
      ],
      nova_categoria: "",
    };
  },

  methods: {
    salvar() {
      if (this.nova_categoria !== "") {
        const novo_id = uuidv4();
        this.categorias.push({
          id: novo_id,
          nome: this.nova_categoria,
        });
        this.nova_categoria = "";
      }
    },
    excluir(categorias) {
      const indice = this.categorias.indexOf(categorias);
      this.categorias.splice(indice, 1);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Gerenciamento de Categorias</h2>
    </div>
    <div class="form-input">
      <input type="text" v-model="nova_categoria" placeholder="categoria..." />
      <button @click="salvar">Adicionar</button>
    </div>
    <div class="list-categorias">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Descrição</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="categorias in categorias" :key="categorias.id">
            <td>{{ categorias.id }}</td>
            <td>{{ categorias.nome }}</td>
            <td>
              <button class="delete" @click="excluir(categorias)">
                Excluir
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style>
.container {
  width: 100%;
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
  width: 60%;
  height: 40px;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 0 10px;
}

.form-input button {
  margin-left: 1%;
  width: 20%;
  height: 40px;
  border: 1px solid #fca311;
  border-radius: 10px;
  background-color: #fca311;
  color: white;
  font-weight: bold;
  cursor: pointer;
}

.list-categorias {
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
  padding: 10px;
  font-weight: bold;
}

table tr td {
  border: 1px solid #ccc;
  padding: 10px;
}
.delete {
  background-color: #14213d;
  color: #fca311;
  border: #fca311;
  border-radius: 20px;
  width: 50%;
  height: 30px;
}

table tr:nth-child(odd) {
  background-color: #ccc;
}
</style>
