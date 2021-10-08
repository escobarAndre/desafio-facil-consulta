<template>
  <div id="app">
    <form-one @evento-success="success" v-if="page == 1"></form-one>
    <form-two @evento-success="success" v-if="page == 2"></form-two>
    <form-tree
      v-if="page == 3"
      :Nome="this.Nome"
      :CPF="this.CPF"
      :Celular="this.Celular"
      :Cidade="this.Cidade"
      :Estado="this.Estado"
      :Especialidade="this.Especialidade"
      :Valor="this.Valor"
      :FormaDePagamento="this.FormaDePagamento"
      :FormaDePagamentoParc="this.FormaDePagamentoParc"
      @evento-success="success"
    ></form-tree>
    <success v-if="page == 4"></success>


  </div>
</template>

<script>
import formOne from "./components/page-one.vue";
import formTwo from "./components/page-two.vue";
import formTree from "./components/page-tree.vue";
import success from './components/page-four.vue'

export default {
  beforeDestroy() {
    this.success();
  },

  name: "App",
  components: { formOne, formTwo, formTree, success },
  data() {
    return {
      page: 1,
      Nome: "",
      CPF: "",
      Celular: "",
      Cidade: "",
      Estado: "",
      Especialidade: "",
      Valor: "",
      FormaDePagamento: "",
      FormaDePagamentoParc: "",
    };
  },
  methods: {
    success(payload) {
      if (payload.page == 1) {
        this.page = 2;
        this.Nome = payload.nome;
        this.CPF = payload.cpf;
        this.Celular = payload.celular;
        this.Cidade = payload.cidade;
        this.Estado = payload.estado;
      } else if (payload.page == 2) {
        this.page = 3;
        this.Especialidade = payload.especialidade;
        this.Valor = payload.valor;
        this.FormaDePagamento = payload.formaDePagamento;
        this.FormaDePagamentoParc = payload.formaDePagamentoParc;
      } else if (payload.verifique == 1) {
        this.page = payload.pageVerificada
        console.log('work verif 1')
      } else if (payload.verifique == 2) {
        this.page = payload.pageVerificada
        console.log('work verif 2')

      }
    },
  },
};
</script>

<style>
#app {
  margin: 0;
  padding: 1rem;
  width: 100vw;
  height: auto;
  min-height: 100vh;
  background-color: #ffe766;
}

h1,
h2,
h3,
h4,
h5 {
  font-family: "Comfortaa", cursive;
}

button {
  font-family: "Comfortaa", cursive;
}

p {
  font-family: "Open Sans", sans-serif;
}

@media (max-width: 500px) {
    #app {
      padding: 3rem 0 0 0 ;
    }
}
</style>
