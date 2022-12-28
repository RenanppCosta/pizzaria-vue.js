<template>
    <div>
        <Message :msg="msg" v-show="msg" />
        <table>
            <thead>
                <tr>
                    <th>#</th>
                    <th>Cliente</th>
                    <th>Tamanho</th>
                    <th>Sabor</th>
                    <th>Observação</th>
                    <th>Status</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="pizza in pizzas" :key="pizza.id">
                    <td>{{pizza.id}}</td>
                    <td>{{pizza.name}}</td>
                    <td>{{pizza.tamanho}}</td>
                    <td>{{pizza.sabor}}</td>
                    <td>{{pizza.observacao}}</td>
                    <td>
                        <select name="status" class="status-order" @change="updatePizza($event, pizza.id)">
                            <option v-for="sts in status"  :value="sts.tipo" :key="sts.id" :selected="pizza.status == sts.tipo">{{sts.tipo}}</option>
                        </select>
                        <button @click="deletePizza(pizza.id)">Cancelar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
import Message from "./Message.vue"

export default {
    name:"Dashboard",
    data(){
        return{
            pizzas: null,
            pizzas_id: null,
            status: [],
            msg: null
        }
    },
    methods: {
        async getPedidos(){
            const req = await fetch("http://localhost:3000/pizzas");

            const data = await req.json();

            this.pizzas = data;

            this.getStatus();
        },
        async getStatus(){
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;
        },
        async deletePizza(id){
            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method: "DELETE"
            })

            const res = await req.json();

            this.msg = `Pedido removido com sucesso!`;
            setTimeout(() => this.msg = "", 5000);

            this.getPedidos();
        },
        async updatePizza(event, id){
            const option = event.target.value;

            const dataJson = JSON.stringify({status: option});

            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method: "PATCH",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            });

            const res = await req.json();

            this.msg = `O pedido ${res.id} foi atualizado para ${res.status} com sucesso!`;
            setTimeout(() => this.msg = "", 5000);

            console.log(res)
        }
    },
    mounted(){
        this.getPedidos()
    },
    components:{
        Message
    }
}
</script>

<style scoped>
    table{
        text-align: left;
        border-spacing: 0;
        margin-top: 2rem;
    }

    th, td{
        padding: 0.5rem 2rem;
    }

    th{
        border-bottom: 2px solid #0e0e0e;
    }

    td{
        border-bottom: 2px solid #d1c3c3;
    }

    button{
        border: 1px solid #0e0e0e;
        color: #0e0e0e;
        background-color: #ffed00;
        padding: 0.6rem;
        border-radius: 1rem;
        font-weight: 500;
        transition: 0.5s;
        cursor: pointer;
        margin-left: 1rem;
    }

    button:hover{
        background-color: #0e0e0e;
        color: #ffed00;
        border: 1px solid #0e0e0e;
    }

    select{
        padding: 0.5rem;
    }

    @media(max-width:1150px){
        th, td{
        padding: 1rem 0.5rem;
    }

    select{
        padding: 0.2rem;
    }

    button{
        padding: 0.3rem;
    }
    }

    @media(max-width:550px){
        th, td{
        font-size: 12px;
        padding: 0.2rem;
    }

    button{
        font-size: 12px;
    }

    select{
        font-size: 12px;
        padding: 0;
    }
    }
</style>