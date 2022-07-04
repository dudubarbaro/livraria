<script>
import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    return {
      autores: [
        { id: "8ae6623d-5462-4774-b5e1-e263c5d2d367", nome: "Autor 1" },
      ],
      novo_autor: "",
    };
  },

  methods: {
    salvar() {
      if (this.novo_autor !== "") {
        const novo_id = uuidv4();
        this.autores.push({
          id: novo_id,
          nome: this.novo_autor,
        });
        this.novo_autor = "";
      }
    },
    excluir(autores) {
      const indice = this.autores.indexOf(autores);
      this.autores.splice(indice, 1);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Gerenciamento de Autores</h2>
    </div>
    <div class="form-input">
      <input type="text" v-model="novo_autor" placeholder="autor..." />
      <button @click="salvar">Adicionar</button>
    </div>
    <div class="list-autores">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Nome</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="autores in autores" :key="autores.id">
            <td>{{ autores.id }}</td>
            <td>{{ autores.nome }}</td>
            <td>
              <button class="delete" @click="excluir(autores)">Excluir</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style>
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

.list-autores {
  display: flex;
  justify-content: center;
}

table {
  width: 50%;
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

table tr:nth-child(odd) {
  background-color: #ccc;
}
.delete {
  background-color: #14213d;
  color: #fca311;
  border: #fca311;
  border-radius: 20px;
  width: 50%;
  height: 30px;
}
</style>
