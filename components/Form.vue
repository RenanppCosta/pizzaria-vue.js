<template>
    <div>
        <Message :msg="msg" v-show="msg"/>
        <div id="container_form">
            <form @submit="orderPlaced">

                <div class="container_input">
                    <label for="name">Nome do Cliente</label>
                    <input type="text" id="name" name="name" v-model="name" placeholder="Digite seu Nome">
                </div>
                
                <div class="container_input">
                    <label for="size">Escolha o tamanho da pizza:</label>
                    <select name="tamanho" id="tamanho" v-model="tamanho">
                        <option v-for="tamanho in tamanhos" :key="tamanho.id" :value="tamanho.tipo">{{tamanho.tipo}} : {{tamanho.preco}}</option>
                    </select>
                </div>

                <div class="container_input">
                    <label for="sabor">Escolha o sabor da pizza:</label>
                    <select name="sabor" id="sabor" v-model="sabor">
                        <option v-for="sabor in sabores" :key="sabor.id" :value="sabor.tipo">{{sabor.tipo}}</option>
                    </select>
                </div>

                <div class="container_input">
                    <label for="observacao">Observação</label>
                    <input type="text" name="observacao" id="observacao" v-model="observacao">
                </div>

                <button type="submit">Fazer pedido</button>
            </form>
        </div>
    </div>
</template>

<script>
import Message from "./Message.vue"

export default {
    name:"Form",
    data(){
        return{
            tamanhos: null,
            sabores: null,
            observacao: null,
            name: null,
            status: "Solicitado",
            msg: null,
            tamanho: null,
            sabor: null,
            preco: null
        }
    },
    methods:{
        async getTamanhos(){
            const req = await fetch("http://localhost:3000/tamanhos");
            const data = await req.json();

            this.tamanhos = data;

        },
        async getSabores(){
            const req = await fetch("http://localhost:3000/sabores");
            const data = await req.json();

            this.sabores = data;
        },
        async orderPlaced(e){
            e.preventDefault();
            
            const data = {
                name: this.name,
                tamanho: this.tamanho,
                sabor: this.sabor,
                observacao: this.observacao,
                status: "Solicitado"
            }

            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/pizzas" , {
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            });

            const res = await req.json();
            
            this.msg = `${res.name} seu pedido foi realizado com sucesso!`;
            setTimeout(() => this.msg = "", 5000);

            this.sabor = "";
            this.tamanho = "";
            this.name = "";
            this.observacao = "";
        }
    },
    mounted(){
        this.getTamanhos(),
        this.getSabores()
    },
    components:{
        Message
    }
}
</script>

<style scoped>
    form{
        margin-top: 1rem;
        display: flex;
        flex-direction: column;
    }

    .container_input{
        margin-bottom: 1rem;
        display: flex;
        flex-direction: column;
    }

    input, select{
        padding: 0.3rem;
    }

    label{
        margin-bottom: 0.7rem;
        padding-left: 0.6rem;
        border-left: 2px solid #ffed00;
        font-size: 1.2rem;
        font-weight: 500;
    }

    button{
        border: none;
        background-color: #0e0e0e;
        color: #ffed00;
        padding: 1rem;
        font-size: 1.2rem;
        font-weight: 500;
        border-radius: 1rem;
        transition: 0.5s;
        cursor: pointer;
    }

    button:hover{
        background-color: transparent;
        color: #0e0e0e;
        border: 1px solid #0e0e0e;
    }
</style>