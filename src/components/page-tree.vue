<template>
  <div>
    <div id="form" class="pt-5 pb-1 px-5 row shadow">
      <h2 class="mb-5">Revisão do cadastro</h2>
      <div class="col coluna-1">
          <p>Nome completo</p>
          <p class="p-sub-text">{{Nome}}</p>
          <p>CPF</p>
          <p class="p-sub-text">{{CPF}}</p>
          <p>Número de celular ou telefone</p>
          <p class="p-sub-text">{{Celular}}</p>
          <p>Estado/Cidade</p>
          <p class="p-sub-text">{{Estado}}/{{Cidade}}</p>
          <p>Especialidade principal</p>
          <p class="p-sub-text">{{Especialidade}}</p>
          <p>Preço da consulta</p>
          <p class="p-sub-text">{{Valor}}</p>
          <p>Formas de pagamento da consulta</p>
          <p class="p-sub-text">{{FormaDePagamento.toString()}} {{` ${FormaDePagamentoParc.toString()}`}}</p>
          
       
        <buttonFC
          :page="3"
          :numberBtn="5"
          :especialidade="especialidade"
          :valor="valor"
          :formaPagamento="formaPagamento"
          :formaPagamentoParc="formaPagamentoParc"
          :color="'#FBDE40'"
          @evento-do-filho="goFinalPage"
          texto="CADASTRAR PROFISSIONAL"
          id="botao"
          class="mt-2 mb-3 w-75"
        ></buttonFC>
        <buttonFC
          :page="3"
          :numberBtn="6"
          :especialidade="especialidade"
          :valor="valor"
          :formaPagamento="formaPagamento"
          :formaPagamentoParc="formaPagamentoParc"
          @evento-do-filho="backPageOne"
          texto="Editar cadastro"
          id="botao-1"
          class="mt-2 mb-3 w-75"
        ></buttonFC>
      </div>
      <div class="col coluna-2">
        <img src="../assets/desktop-pagina-3.png" alt="" />
      </div>
    </div>

  </div>
</template>

<script>
import buttonFC from "./button.vue";
import { mask } from "vue-the-mask";

export default {
  methods: {
    backPageOne(payload) {
      console.log(payload)
      console.log('work payload')
      this.page(payload.page, 1)
    },
    goFinalPage(payload) {
      console.log(payload)
      console.log('work payload btn 1')
      this.page(payload.page, 2)

    },
    page(pageVerificada, verificação) {
      this.$emit('evento-success', {pageVerificada: pageVerificada, verifique: verificação})
      console.log('work page')
    }
  },
  directives: { mask },
  components: {
    buttonFC,
  },
  data() {
    return {
    };
  },
  props: {
      Nome: String,
      CPF: String,
      Celular: String,
      Cidade: String,
      Estado: String,
      Especialidade: String,
      Valor: String,
      FormaDePagamento: Array,
      FormaDePagamentoParc: String
  }
};
</script>

<style scoped>
#form {
  width: 65vw;
  height: auto;
  background-color: #ffffff;
  border-radius: 1rem;
  margin: 0 auto;
  left: 17%;
  top: 3.5%;
}

h2 {
  color: #483698;
}

p {
  color: #282828;
  font-size: 1rem;
  font-weight: 600;
}

.p-sub-text{
    font-weight: 300;
}

label {
  font-family: "Open Sans", sans-serif;
  font-size: 0.9rem;
}

#botao {
  background-color: #FBDE40;
  color: #483698;
  border: none;
}

#botao-1{
    background-color: white;
    color: #483698;
    border: none;
    
}

img {
  max-width: 130%;
  position: relative;
  top: 20%;
  left: -20%;
}


@media (max-width: 480px) {
  #form {
    width: 100vw;
    height: 95vh;
    background-color: #ffffff;
    border-radius: 5rem 5rem 0 0 ;
    margin: 0 auto;
    padding: 3rem 1rem!important;
  }

  h2{
    text-align: center;
    padding: 0;
    margin: 0;
    height: 1rem;
  }

  .coluna-1{
    width: 50%;
  }

  .coluna-2{
    width: auto;
    display: none;
  }

  .label-mb{
    margin-top: 2rem!important;
  }

  .progress-bar-group{
    margin-left: 10%;
  }

  #botao{
    margin-left: 10%;
  }

  #botao-1{
    margin-left: 10%;
  }

  img{
    display: none;
  }
}
</style>