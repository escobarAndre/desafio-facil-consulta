<template>
  <div>
    <div id="form" class="pt-5 pb-1 px-5 row shadow">
      <h2>Sobre o atendimento</h2>
      <div class="col coluna-1">
        <p class="my-3">Detalhes do atendimento</p>
        <b-form class="mb-4">
          <div class="select-div w-100">
            <label class="mt-2 mb-1 label-mb">Especialidade principal*</label>
            <b-form-select
              class="select mb-2 w-100"
              v-model="especialidade"
              :options="options"
            ></b-form-select>
            <p v-if="errorEspecialidade == false" class="form-error">
              Por favor, escolha uma especialidade.
            </p>
          </div>
          <label class="sr-only label-mb" for="inline-form-input-username"
            >Informe o preço da consulta*</label
          >

          <div class="input-group mb-3">
            <div class="input-group-prepend">
              <span
                style="backgroundcolor: #483698; color: white"
                class="input-group-text"
                id="basic-addon1"
                >R$</span
              >
            </div>
            <input
              v-model="valor"
              v-mask="['##,##', '###,##']"
              type="price"
              min="1"
              step="any"
              class="form-control"
              placeholder="Valor"
              aria-label="Informa o preço da consulta*"
              aria-describedby="basic-addon1"
            />
          </div>
          <p v-if="errorValor == false" class="form-error">
              Por favor, insira um valor válido. (entre 30,00 e 350,00 com vírgula)
            </p>
          <p style="fontweight: 400; fontsize: 1rem label-mb">
            Formas de pagamento da consulta
          </p>
          <div class="container text-left py-1 w-100 my-2 input-checkbox">
            <b-form-checkbox
              id="checkbox-1"
              v-model="formaPagamento"
              name="checkbox-1"
              value="Pix"
              v-bind:disabled="disabledPix"
              :checked="(debitoChecked = true)"
            >
              Pix
            </b-form-checkbox>
          </div>
          <div class="container text-left py-1 w-100 my-2 input-checkbox">
            <b-form-checkbox
              id="checkbox-1"
              v-model="formaPagamento"
              name="checkbox-1"
              value="Dinheiro"
              v-bind:disabled="disabledDin"
              unchecked-value="not_accepted"
            >
              Dinheiro
            </b-form-checkbox>
          </div>
          <div class="container text-left py-1 w-100 my-2 input-checkbox">
            <b-form-checkbox
              id="checkbox-1"
              v-model="formaPagamento"
              name="checkbox-1"
              value="Débito"
              v-bind:disabled="disabledDeb"
            >
              Cartão débito
            </b-form-checkbox>
          </div>
          <div
            class="container text-left py-1 w-100 my-2 input-checkbox-credit"
          >
            <b-form-checkbox
              id="checkbox-1"
              v-model="formaPagamento"
              name="checkbox-1"
              value="Crédito"
              v-bind:disabled="disabledCred"
            >
              Cartão crédito
            </b-form-checkbox>
            <div v-if="credit == true" class="px-3">
              <b-form-group
                label="Parcelado em:"
                v-slot="{ ariaDescribedby }">
                <b-form-radio-group
                  id="radio-group-1"
                  v-model="formaPagamentoParc"
                  :options="parcelado"
                  :aria-describedby="ariaDescribedby"
                  name="radio-options"
                ></b-form-radio-group>
              </b-form-group>
              <p v-if="errorFormaDePagamentoParc == false" class="form-error">
              Por favor, escolha uma forma de parcelamento.
            </p>
            </div>
          </div>
          <p v-if="errorFormaDePagamento == false" class="form-error">
              Por favor, escolha uma forma de pagamento.
            </p>
        </b-form>
        <div style="display: flex" class="mt-4 progress-bar-group w-100 d-flex">
          <div class="progress-bar w-25"></div>
          <div class="progress-bar-2 w-25"></div>
          <div style="textAlign: right" class="w-25">
            <h5 >2 de 2</h5>
          </div>
        </div>
        <buttonFC
          v-bind:page="2"
          v-bind:especialidade="especialidade"
          v-bind:valor="valor"
          v-bind:formaPagamento="formaPagamento"
          v-bind:formaPagamentoParc="formaPagamentoParc"
          @evento-do-filho="errorMensages"
          texto="PRÓXIMO"
          id="botao"
          class="mt-2 mb-3 w-75"
        ></buttonFC>
      </div>
      <div class="col coluna-2">
        <img src="../assets/desktop-pagina-2.png" alt="" />
      </div>
    </div>
    {{valideFormaPagamento()}}
  </div>
</template>

<script>
import buttonFC from "./button.vue";
import { mask } from "vue-the-mask";

export default {
  methods: {
    errorMensages(payload) {
      this.errorEspecialidade = payload.errorEspecialidade
      this.errorValor = payload.errorValor
      this.errorFormaDePagamento = payload.errorFormaDePagamento
      this.errorFormaDePagamentoParc = payload.errorFormaDePagamentoParc
      this.valideSuccess(payload.success)
    },
    valideSuccess(success) {
      if(success == true) {
        this.$emit('evento-success' , {success: this.success, page: 2, especialidade: this.especialidade, valor: this.valor, formaDePagamento: this.formaPagamento, formaDePagamentoParc: this.formaPagamentoParc})
      } 
    },
    valideFormaPagamento() {
      if (this.formaPagamento.length == 2) {
        if (
          (this.formaPagamento.indexOf("Crédito") == -1) &
          (this.formaPagamento.indexOf("Débito") == -1)
        ) {
          this.disabledCred = true;
          this.disabledDeb = true;
        } else if (
          (this.formaPagamento.indexOf("Crédito") == -1) &
          (this.formaPagamento.indexOf("Pix") == -1)
        ) {
          this.disabledPix = true;
          this.disabledCred = true;
        } else if (
          (this.formaPagamento.indexOf("Crédito") == -1) &
          (this.formaPagamento.indexOf("Dinheiro") == -1)
        ) {
          this.disabledCred = true;
          this.disabledDin = true;
        }
      } else if (this.formaPagamento.indexOf("Crédito") > -1) {
        console.log('work')
        this.disabledDeb = true;
        this.disabledPix = true;
        this.disabledDin = true;
        this.credit = true;
      } else if (this.formaPagamento.length == 1) {
        this.disabledDeb = false;
        this.disabledPix = false;
        this.disabledDin = false;
        this.disabledCred = false;
      } else if (this.formaPagamento.length == 0) {
        this.disabledDeb = false;
        this.disabledPix = false;
        this.disabledDin = false;
        this.disabledCred = false;
        this.credit = false;
      } 
    },
  },
  directives: { mask },
  components: {
    buttonFC,
  },
  data() {
    return {
      disabledDeb: false,
      disabledPix: false,
      disabledDin: false,
      disabledCred: false,
      disabledCred1: false,
      disabledCred2: false,
      disabledCred3: false,

      especialidade: "",
      valor: "",
      formaPagamento: [],
      formaPagamentoParc: '',
      credit: false,
      errorCPF: true,
      errorNome: true,
      errorCel: true,
      errorEstado: true,
      errorCidade: true,
      errorEspecialidade: true,
      errorValor: true,
      errorFormaDePagamento: true,
      errorFormaDePagamentoParc: true,
      nome: "",
      cpf: "",
      celular: "",
      cidade: "",
      estado: "",
      show: true,
      teste: false,
      options: [
        { value: "", text: "Selecione a especialidade", disabled: true },
        { value: "Cardiologia", text: "Cardiologia" },
        { value: "Dermatologia", text: "Dermatologia" },
        { value: "Neurologia", text: "Neurologia" },
        { value: "Oftalmologia", text: "Oftalmologia" },
        { value: "Psiquiatria", text: "Psiquiatria" },
        { value: "Urologia", text: "Urologia" },
      ],
      parcelado: [
          { text: 'à vista', value: 'à vista' },
          { text: '2x sem juros', value: '2x sem juros' },
          { text: '3x sem juros', value: '3x sem juros' },
          { text: '4x sem juros', value: '4x sem juros'},
        ]
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
  padding: 1rem;
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


.input-text {
  background-color: #483698;
}

.input-checkbox {
  height: 2rem;
  background-color: #b9b9b9;
  border-radius: 0.3rem;
}

.input-checkbox-credit {
  height: auto;
  background-color: #b9b9b9;
  border-radius: 0.3rem;
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

.progress-bar-2 {
  height: 1.4rem;
  background-color: #483698;
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