<script>
import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    return {
      editoras: [
        {
          id: "8ae6623d-5462-4774-b5e1-e263c5d2d367",
          nome: "Editora 1",
          site: "www.",
        },
      ],
      nova_editora: "",
      novo_site: "",
    };
  },

  methods: {
    salvar() {
      if (this.nova_editora !== "") {
        const novo_id = uuidv4();
        this.editoras.push({
          id: novo_id,
          nome: this.nova_editora,
          site: this.novo_site,
        });
        this.nova_editora = "";
        this.novo_site = "";
      }
    },
    excluir(editoras) {
      const indice = this.editoras.indexOf(editoras);
      this.editoras.splice(indice, 1);
    },
  },
};
</script>

<template>
  <div class="container">
    <div class="title">
      <h2>Gerenciamento de Editoras</h2>
    </div>
    <div class="form-input">
      <input type="text" v-model="nova_editora" placeholder="editora..." />
      <input type="text" v-model="novo_site" placeholder="site..." />
      <button @click="salvar">Adicionar</button>
    </div>
    <div class="list-editoras">
      <table>
        <thead>
          <tr>
            <th>ID</th>
            <th>Nome</th>
            <th>Site</th>
            <th>Ações</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="editoras in editoras" :key="editoras.id">
            <td>{{ editoras.id }}</td>
            <td>{{ editoras.nome }}</td>
            <td>{{ editoras.site }}</td>
            <td>
              <button class="delete" @click="excluir(editoras)">Excluir</button>
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

.list-editoras {
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
</style>
