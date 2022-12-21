<template>
    <div>
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
                    <td class="status">
                        <select name="status" class="status-order">
                            <option value="">Status do pedido</option>
                        </select>
                        <button>Cancelar</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name:"Dashboard",
    data(){
        return{
            pizzas: null,
            pizzas_id: null,
            status: []
        }
    },
    methods: {
        async getPedidos(){
            const req = await fetch("http://localhost:3000/pizzas");

            const data = await req.json();

            this.pizzas = data;

            console.log(data)
        }
    },
    mounted(){
        this.getPedidos()
    }
}
</script>

<style scoped>
    table{
        text-align: left;
        border-spacing: 0;
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

</style>