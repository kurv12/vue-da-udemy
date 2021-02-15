<template>
  <div id="app">
    <h3>Cadastro:</h3>
    <small id="nomeErro" v-show="deuErro">Nome inválido!</small><br />
    <input type="text" placeholder="nome" v-model="nomeField" /> <br />
    <input type="text" placeholder="email" v-model="emailField" /><br />
    <input type="number" placeholder="idade" v-model="idadeField" /><br />
    <button @click="cadastrarUsuario">Cadastrar</button>
    <hr />
    <!-- <input type="text" v-model="clienteFabio.nome" /> -->
    <!-- <Cliente :cliente="clienteFabio" :showIdade="true" />
    <Cliente :cliente="clienteFabio" :showIdade="false" />
    <Cliente :cliente="clienteFabio" :showIdade="true" /> -->

    <div v-for="(cliente, index) in orderClientes" :key="cliente.id">
      <h1>{{ index }}</h1>
      <Cliente :cliente="cliente" @meDelete="deletarUsuario" />
      <hr />
    </div>
  </div>
</template>

<script>
import _ from "lodash";
import Cliente from "./components/Cliente";
// import Produto from "./components/Produto";

export default {
  name: "App",
  data() {
    return {
      deuErro: false,
      nomeField: "",
      emailField: "",
      showIdadeField: true,
      idadeField: 0,
      clientes: [
        {
          id: 1,
          nome: "Fábio da silva",
          email: "fabio@gmail.com",
          showIdade: true,
          idade: 23,
        },
        {
          id: 2,
          nome: "Victor costa",
          email: "victor@gmail.com",
          showIdade: true,
          idade: 35,
        },
        {
          id: 3,
          nome: "Maria lopes",
          email: "maria@gmail.com",
          showIdade: true,
          idade: 25,
        },
        {
          id: 4,
          nome: "Elisa Rabello",
          email: "elisa@gmail.com",
          showIdade: true,
          idade: 28,
        },
      ],
    };
  },
  components: {
    Cliente,
    // Produto,
  },
  methods: {
    cadastrarUsuario: function() {
      if (this.nomeField == "" || this.nomeField == " " || this.nomeField < 3) {
        console.log("Erro de validação");
        this.deuErro = true;
      } else {
        this.clientes.push({
          nome: this.nomeField,
          email: this.emailField,
          showIdade: this.showIdadeField,
          idade: this.idadeField,
          id: Date.now(),
        });
        this.nomeField = "";
        this.emailField = "";
        this.idadeField = 0;
        this.deuErro = false;
      }
    },
    deletarUsuario: function($event) {
      console.log("Recebendo evento");
      var id = $event.idDoCliente;
      var novoArray = this.clientes.filter((cliente) => cliente.id != id);
      this.clientes = novoArray;
    },
  },
  computed: {
    orderClientes: function() {
      return _.orderBy(this.clientes, ["nome"], ["asc"]);
    },
  },
};
</script>

<style>
#nomeErro {
  color: red;
}
</style>
