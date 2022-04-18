<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <div>
            <form id="burguer-form" @submit="createBurguer">
                <div class="input-container">
                    <label for="nome">Nome do Cliente: </label>
                    <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o seu nome...">
                </div>
            
                <div class="input-container">
                    <label for="pao">Escolha o tipo de pão: </label>
                    <select name="pao" id="pao" v-model="pao">
                        <option value="">Selecione o seu pão</option>
                        <option v-for="pao in paes" :key="pao.id" :value="pao.tipo"> {{ pao.tipo }}</option>
                    </select>
                </div>

                <div class="input-container">
                    <label for="carne">Escolha a carne: </label>
                    <select name="carne" id="carne" v-model="carne">
                        <option value="">Selecione tipo de carne</option>
                        <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo"> {{ carne.tipo }}</option>
                    </select>
                </div>

                <div id="opcionais-container" class="input-container">
                    <label id="opcionais-title" for="opcionais">Selecione os opcionais: </label>
                    <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
                        <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
                        <span>{{ opcional.tipo }}</span>
                    </div>
                </div>

                <div class="input-container">
                    <input type="submit" class="submit-btn" value="Criar meu Burguer">
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import Message from "./Message.vue";

export default {
    name: "BurguerForm",
    data() {
        return {
            paes: null,
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null,
            carne: null,
            opcionais: [],
            msg: null
        }
    },
    methods: {
        async getIngredientes() {

            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();

            this.paes = data.paes;
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;

        },
        async createBurguer(e) {

            e.preventDefault();

            const data = {
                nome: this.nome,
                pao: this.pao,
                carne: this.carne,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }

            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json"
                },
                body: dataJson
            });

            const res = await req.json();
            
            // Colocar uma msg do sistema
            this.msg = `Pedido Nª ${res.id} realizado com sucesso!`;

            //limpar msg
            setTimeout(() => {
                this.msg = "";
            }, 3000);

            // limpar os campos
            this.nome = "";
            this.pao = "";
            this.carne = "";
            this.opcionais = "";
        }
    },
    mounted() {
        this.getIngredientes();
    },
    components: {
        Message
    }
}
</script>

<style scoped>
   #burguer-form {
       max-width: 400px;
       margin: 0 auto;
       display: flex;
       flex-direction: column;
       align-items: center;
   }

   .input-container {
       display: flex;
       flex-direction: column;
       margin-bottom: 20px;
   }

   label {
       font-weight: bold;
       margin-bottom: 15px;
       color: #222;
       padding: 5px 10px;
       border-left: 4px solid #FCBA03;
   }

   #opcionais-container label {
       font-weight: bold;
       margin-bottom: 15px;
       color: #222;
       padding: 4px 10px;
       border-left: 0px solid #FCBA03;
   }

   input, select {
       padding: 5px 10px;
       width: 300px;
       box-shadow: 0 0 0 0;
       border: 0 none;
       outline: 0;
   }

   #opcionais-container {
       flex-direction: row;
       flex-wrap: wrap;
   }

   #opcionais-title {
       display: flex;
       width: 100%;
       justify-content: center;
   }

   .checkbox-container {
       display: flex;
       align-items: center;
       width: 50%;
       margin-bottom: 15px;
       justify-content: center;
   }

   .checkbox-container span, 
   .checkbox-container input {
       width: 100px;
   }

   .checkbox-container span {
       margin-left: 5px;
       font-weight: bold;
   }

   .submit-btn {
       background-color: #222;
       color: #FCBA03;
       font-weight: bold;
       border-radius: 25px;
       border: 2px solid #222;
       padding: 10px;
       font-size: 16px;
       margin: 0 auto;
       cursor: pointer;
       transition: .5s;
   }

   .submit-btn:hover {
       background-color: transparent;
       color: #222;
   }
</style>
