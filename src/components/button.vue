<template>
  <b-button @click="validarDados()" pill>{{ texto }}</b-button>
</template>

<script>
export default {
    data() {
        return {
            errorNome: true,
            errorCPF: true,
            errorCel: true,
            errorEstado: true,
            errorCidade: true,
            errorEspecialidade: true,
            errorValor: true,
            errorFormaDePagamento: true,
            errorFormaDePagamentoParc: true
        }
    },
    props: {
        texto: String,
        page: Number, 
        numberBtn: Number,
        nome: String,
        cpf: String,
        celular: String, 
        estado: String,
        cidade: String,
        especialidade: String,
        valor: String,
        formaPagamento: Array,
        formaPagamentoParc: String,
        color: String
    },
    methods: {
        validarDados() {
            console.log('click work')
            if(this.page === 1) {
                console.log('work page one')
                this.valideNome()
                this.valideCPF()
                this.valideCelular()
                this.valideEstado()
                this.valideCidade()
                this.error()

            } else if (this.page === 2) {
                console.log( 'work page two')
                this.valideEspecialidade()
                this.valideValor()
                this.valideFormaDePagamento()
                this.valideFormaDePagamentoParc()
                this.error2()
            } else if (this.page === 3) {
                console.log('work page tree')
                if(this.numberBtn === 5) {
                    console.log('work btn 1')
                    this.goFinalPage()
                    
                } else if (this.numberBtn === 6) {
                    
                    this.backPageOne()
                    console.log('work btn 2')

                    
                }
            }
        },
        valideFormaDePagamentoParc() {
            if (this.formaPagamento.indexOf("Crédito") > -1 & this.formaPagamentoParc.length == 0) {
                this.errorFormaDePagamentoParc = false
            } else if (this.formaPagamento.indexOf("Crédito") > -1 & this.formaPagamentoParc.length > 1) { this.FormaDePagamentoParc = true}
        },
        valideFormaDePagamento() {
            if (this.formaPagamento.length == 0) {
                this.errorFormaDePagamento = false
            } else { this.errorFormaDePagamento = true}
        },
        valideValor() {
            if (this.valor.length == 5) {
                let valor = this.valor.slice(0, 2)
                let valorFinal = parseInt(valor)
                if (valorFinal < 30) {
                    this.errorValor = false;
                } else { this.errorValor = true}

            } else if (this.valor.length == 6) { 
                let valor = this.valor.slice(0, 3)
                let valorFinal = parseInt(valor)
                if (valorFinal > 350) {
                    this.errorValor = false;
                } else { this.errorValor = true}
            } else if (this.valor.length < 5 | this.valor.length > 6) {
                this.errorValor = false;
            } else { this.errorValor = true}
        },
        valideEspecialidade() {
            if(this.especialidade == '') {
                this.errorEspecialidade = false
            } else { this.errorEspecialidade = true }
        },
        valideNome() {
            if ((this.nome.length > 48) | (this.nome.length < 3)) {
                this.errorNome = false
                } else { this.errorNome = true}
        },
        valideCPF() {
            if (this.cpf == "111.111.111-11" | this.cpf == '222.222.222-22' | this.cpf == '333.333.333-33' | this.cpf == '444.444.444-44' | this.cpf == '555.555.555-55' | this.cpf == '666.666.666-66' | this.cpf == '777.777.777-77' | this.cpf == '888.888.888-88' | this.cpf == '999.999.999-99' | this.cpf == '000.000.000-00' | this.cpf.length > 14 | this.cpf.length < 14 ) {
                this.errorCPF = false
                } else { this.errorCPF = true}
        },
        valideCelular() {
            if (this.celular == "(11) 11111-1111" | this.celular == '(22) 22222-2222' | this.celular == '(33) 33333-3333' | this.celular == '(44) 44444-4444' | this.celular == '(55) 55555-5555' | this.celular == '(66) 66666-6666' | this.celular == '(77) 77777-7777' | this.celular == '(88) 88888-8888' | this.celular == '(99) 99999-9999' | this.celular == '(00) 00000-0000' | this.celular.length > 15 | this.celular.length < 15 ) {
                this.errorCel = false
                } else { this.errorCel = true}
        },
        valideEstado() {
            if(this.estado.length == 0) {
                this.errorEstado = false
            } else { this.errorEstado = true}
        },
        valideCidade() {
            if(this.cidade.length == 0) {
                this.errorCidade = false
            } else { this.errorCidade = true}
        },
        error() {
            if(this.errorNome == true & this.errorCPF == true & this.errorCel == true & this.errorEstado == true & this.errorCidade == true) {
                this.$emit('evento-do-filho', { errorNome: this.errorNome, errorCPF: this.errorCPF, errorCel: this.errorCel, errorEstado: this.errorEstado, errorCidade: this.errorCidade, success: true})
                } 
            else {
                    this.$emit('evento-do-filho', { errorNome: this.errorNome, errorCPF: this.errorCPF, errorCel: this.errorCel, errorEstado: this.errorEstado, errorCidade: this.errorCidade})
                    
                }
        }, 
        error2() {
            if(this.errorEspecialidade == true & this.errorValor == true & this.errorFormaDePagamento == true & this.errorFormaDePagamentoParc == true) {
                this.$emit('evento-do-filho', { errorEspecialidade: this.errorEspecialidade, errorValor: this.errorValor, errorFormaDePagamento: this.errorFormaDePagamento, errorFormaDePagamentoParc: this.errorFormaDePagamentoParc, success: true })
                } 
            else {
                    this.$emit('evento-do-filho', { errorEspecialidade: this.errorEspecialidade, errorValor: this.errorValor, errorFormaDePagamento: this.errorFormaDePagamento, errorFormaDePagamentoParc: this.errorFormaDePagamentoParc })
                }
        },
        backPageOne() {
            this.page = 1
            this.$emit('evento-do-filho', {page: this.page})
            console.log('work back page one')
        },
        goFinalPage() {
            this.page = 4
            this.$emit('evento-do-filho', {page: this.page})
        }
    }

}
</script>

<style scoped>

</style>