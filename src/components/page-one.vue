<template>
    <div id="form" class="pt-5 pb-1 px-5 row shadow">
      <h2>Sobre o profissional</h2>
      <div class="col coluna-1">
        <p class="my-3">Dados do profissional</p>
        <b-form class="mb-4">
          <label class="mb-2" for="nome-completo">Nome completo*</label>
          <b-form-input
            type="text"
            placeholder="Digite o nome completo"
            class="form"
            v-model="nome"
          ></b-form-input>
          <p v-if="errorNome == false" class="form-error">
            Por favor, insira um nome válido
          </p>
          <label class="mt-2 label-mb" for="nome-completo">CPF*</label>
          <b-form-input
            v-mask="'###.###.###-##'"
            type="tel"
            placeholder="Digite um CPF"
            class="form w-75"
            v-model="cpf"
          ></b-form-input>
          <p v-if="errorCPF == false" class="form-error">
            Por favor, insira um CPF válido
          </p>
          <label class="mt-2 label-mb" for="nome-completo">Número de celular*</label>
          <b-form-input
            v-mask="'(##) #####-####'"
            value="cpf"
            type="tel"
            placeholder="(00) 0 0000-0000"
            class="form w-75"
            v-model="celular"
          ></b-form-input>
          <p v-if="errorCel == false" class="form-error">
            Por favor, insira um celular válido
          </p>
          <div class="d-flex">
            <div class="select-div">
              <label class="mt-2 label-mb">Estado*</label>
              <b-form-select
                class="select mb-2 w-75"
                v-model="estado"
                :options="options"
              ></b-form-select>
              <p v-if="errorEstado == false" class="form-error">
                Por favor, escolha um estado
              </p>
            </div>
            <div class="select-div">
              <label class="mt-2 label-mb">Cidade*</label>
              <b-form-select v-model="cidade" class="select mb-2 w-75">
                <b-form-select-option disabled value=""
                  >Cidade</b-form-select-option
                >
                <b-form-select-option
                  v-show="estado === 'Paraná'"
                  value="Londrina"
                  >Londrina</b-form-select-option
                >
                <b-form-select-option
                  v-show="estado === 'Paraná'"
                  value="Maringá"
                  >Maringá</b-form-select-option
                >
                <b-form-select-option
                  v-show="estado === 'Rio Grande do Sul'"
                  value="Pelotas"
                  >Pelotas</b-form-select-option
                >
                <b-form-select-option
                  v-show="estado === 'Rio Grande do Sul'"
                  value="Porto"
                  >Porto Alegre</b-form-select-option
                >
                <b-form-select-option
                  v-show="estado === 'Santa Catarina'"
                  value="Florianópolis"
                  >Florianópolis</b-form-select-option
                >
                <b-form-select-option
                  v-show="estado === 'Santa Catarina'"
                  value="Joinville"
                  >Joinville</b-form-select-option
                >
              </b-form-select>
              <p v-if="errorCidade == false" class="form-error">
                Por favor, escolha uma cidade
              </p>
            </div>
          </div>
        </b-form>
        <div style="display: flex" class="mt-4 progress-bar-group w-100 d-flex">
          <div class="progress-bar w-25"></div>
          <div class="w-25"></div>
          <div style="textalign: right" class="w-25">
            <h5>1 de 2</h5>
          </div>
        </div>
        <buttonFC
          v-bind:page="1"
          v-bind:nome="nome"
          v-bind:cpf="cpf"
          v-bind:celular="celular"
          v-bind:estado="estado"
          v-bind:cidade="cidade"
          @evento-do-filho="errorMensages"
          texto="PRÓXIMO"
          id="botao"
          class="mt-2 mb-3 w-75"
        ></buttonFC>
      </div>
      <div class="col coluna-2">
        <img src="../assets/desktop-pagina-1.png" alt="" />
      </div>
    </div>

</template>

<script>
import buttonFC from "./button.vue";
import { mask } from "vue-the-mask";

export default {
  methods: {
    errorMensages(payload) {
      this.errorNome = payload.errorNome;
      this.errorCPF = payload.errorCPF;
      this.errorCel = payload.errorCel;
      this.errorEstado = payload.errorEstado;
      this.errorCidade = payload.errorCidade;
      this.success = payload.success;
      this.valideSuccess(payload.success);
    },
    valideSuccess(success) {
      if (success == true) {
        this.$emit("evento-success", {
          success: this.success,
          page: 1,
          nome: this.nome,
          cpf: this.cpf,
          celular: this.celular,
          cidade: this.cidade,
          estado: this.estado,
        });
      }
    },
  },
  directives: { mask },
  components: {
    buttonFC,
  },
  data() {
    return {
      success: Boolean,
      errorCPF: true,
      errorNome: true,
      errorCel: true,
      errorEstado: true,
      errorCidade: true,
      nome: "",
      cpf: "",
      celular: "",
      cidade: "",
      estado: "",
      show: true,
      teste: false,
      options: [
        { value: "", text: "Estado", disabled: true },
        { value: "Paraná", text: "Paraná" },
        { value: "Rio Grande do Sul", text: "Rio Grande do Sul" },
        { value: "Santa Catarina", text: "Santa Catarina" },
      ],
    };
  },
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

label {
  font-family: "Open Sans", sans-serif;
  font-size: 0.9rem;
}

.form {
  border: #483698 solid 1px;
}

.form-error {
  font-family: "Open Sans", sans-serif;
  color: #dc3545;
  font-size: 0.7rem;
  margin: 0;
  padding: 0;
}

.select-div {
  display: inline-block;
}

.select {
  height: 2.5rem;
  border: #483698 solid 1px;
  border-radius: 0.2rem;
}

.progress-bar {
  height: 1.4rem;
  background-color: #483698;
  border-radius: 0.3rem 0 0 0.3rem;
}

.progress-bar-group h5 {
  color: #483698;
  font-size: 1rem;
}

#botao {
  background-color: #483698;
}

img {
  max-width: 110%;
  position: relative;
  top: 20%;
  left: 0%;
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
    margin-left: 8%;
  }

  img{
    display: none;
  }
}


</style>