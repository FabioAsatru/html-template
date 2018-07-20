<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card card-default">
                    <div class="card-header">Example Component</div>

                    <div class="card-body">
                        I'm an example componen teste.
                    </div>
                    <ul v-for="uf in optionsEstados" :key="uf">
                        <li>{{ uf }}</li>
                    </ul>
            {{ uf }}
            uf: {{ selectedUF}} <br>
            cidade {{ selectedCidade}} <br>
            bairro {{ selectedBairro }} {{ showBairro() }}<br>

                    <select v-model="selectedUF" id="" @change="onChangeUF">
                        <option v-for="uf in optionsEstados" :key="uf">{{ uf }}</option>
                    </select>
                    <select v-model="selectedCidade" id="" >
                        <option v-for="cidade in optionsCidades" :key="cidade">{{ cidade }}</option>
                    </select>
                    <select v-model="selectedBairro" id="" v-if="showBairro()">
                        <option v-for="bairro in optionsBairros" :key="bairro">{{ bairro }}</option>
                    </select>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        mounted() {
            console.log('Component mounted.')
        },
        data(){
            return{
                guiaMedico:[
                    {
                        nome:"fabio",
                        estado:"AM",
                        cidade:"manaus",
                        bairro:"alvorada"
                    },
                    {
                        nome:"fabio",
                        estado:"AM",
                        cidade:"parintins",
                        bairro:"alvorada A"
                    },{
                        nome:"fabio",
                        estado:"RJ",
                        cidade:"Rio de Janeiro",
                        bairro:"alvorada 1"
                    },
                    {
                        nome:"fabio",
                        estado:"RJ",
                        cidade:"Rio 2",
                        bairro:"alvorada 2"
                    }
                    ,{
                        nome:"fabio",
                        estado:"SP",
                        cidade:"sao paulo",
                        bairro:"alvorada 4"
                    }    
                ],
                selectedUF: "",
                selectedCidade: "",
                selectedBairro: "",
                uf:[]
            }
        },

        computed: {
            optionsEstados() {
                let estados = []

                this.guiaMedico.forEach(element => {
                    if (estados.indexOf(element.estado) == -1 ) {
                        console.log('Add ' + element.estado)
                        estados.push(element.estado)
                    }
                });
                this.uf = estados
                return estados
            },

            optionsCidades() {
                let cidades = []

                this.guiaMedico.forEach(element => {
                    if (element.estado == this.selectedUF) {
                        if (cidades.indexOf(element.cidade) == -1 ) {
                            console.log('Add ' + element.cidade)
                            cidades.push(element.cidade)
                        }
                    }
                    
                });
                return cidades
            },

            optionsBairros() {
                let bairros = []

                this.guiaMedico.forEach(element => {
                    if ((element.estado == this.selectedUF) && 
                    (element.cidade == this.selectedCidade)) 
                    {
                        if (bairros.indexOf(element.bairro) == -1 ) {
                            console.log('Add ' + element.bairro)
                            bairros.push(element.bairro)
                        }
                    }
                    
                });
                return bairros
            },

        },

        methods: {
            onChangeUF() {
                this.selectedCidade = "" // false
                this.selectedBairro = "" // false
            },
            showBairro() {
                return this.selectedCidade
            }

        }
    }
</script>


