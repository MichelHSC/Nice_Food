<template>
    <div id="burger-table">
        <div>
            <Message :msg="msg" v-show="msg" />
            <div id="burger-table-heading">
                <div class="order-id">#:</div>
                <div>Cliente:</div>
                <div>Pão:</div>
                <div>Carne:</div>
                <div>Opcionais:</div>
                <div>Ações:</div>
            </div>
        </div>
        <div id="burger-table-rows">
            <div class="burger-table-row" v-for="burger in burgers" :key="burger.id">
                <div class="order-number">{{ burger.id }}</div>
                <div>{{ burger.nome }}</div>
                <div>{{ burger.pao }}</div>
                <div>{{ burger.carne }}</div>
                <div>
                    <ul>
                        <li id="lista" v-for="(opcionais ,index) in burger.opcionais" :key="index" >
                            {{ opcionais }}
                        </li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="status" @change="updatedBurger($event, burger.id)">
                        <option value="">Selecione</option>
                        <option v-for="s in status" :key="s.id" :value="s.tipo" :selected="burger.status == s.tipo">{{ s.tipo }}</option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                </div>
            </div>
            
        </div>
        
    </div>

</template>
<script>
import Message from './Message.vue';

export default{
    name: 'Dashboard',
    components:{
        Message
    },
    data(){
        return{
            burgers: null,
            burger_id: null,
            status: [],
            msg: null
        }
    },
    methods:{
        async getPedidos(){
            const req = await fetch("http://localhost:3000/burgers");

            const data = await req.json();

            this.burgers = data;

            console.log(this.burgers);

            //resgatar status 
            this.getStatus();
            
        },
        async getStatus(){
            const req = await fetch("http://localhost:3000/status")

            const data = await req.json();

            this.status = data;

        },
        async deleteBurger(id){
            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                method: "DELETE"
            });

            const res = await req.json();

            //Colocar uma msg de sistema
             this.msg = `Pedido Nº ${res.id} deletado`

            //Limpar msg
            setTimeout(() => this.msg = "", 3000);

            this.getPedidos();

        },
        async updatedBurger(event,id){
        
            const option = event.target.value

            const dataJson = JSON.stringify({ status: option});

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "PATCH",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });

            const res = await req.json();

            //Colocar uma msg de sistema
            this.msg = `Pedido Nº ${res.id} Atualizado`

            //Limpar msg
            setTimeout(() => this.msg = "", 3000);
            

        
        }


    },
    mounted(){
        this.getPedidos();
    }
}
</script>

<style scoped>
    #burger-table{
        max-width: 100vw;
        margin: 0 auto;
    }
    #burger-table-heading,
    #burger-table-rows,
    .burger-table-row {
        display: flex;
        flex-wrap: wrap                                                                                                                                                                                               ;
    }
    #burger-table-heading{
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #000;
    }
    #burger-table-heading div,
    .burger-table-row div {
        width: 17%;
        text-align: center;

    }
    .burger-table-row{
        width: 100%;
        padding: 12px;
        border-bottom: 1px solid #ccc;
    }
        
    #burger-table-heading .order-id,
    .burger-table-row .order-number {
        width: 5%;
    } 
    select{
        /* width: 150px ; */
        padding: 12px 5px;
        margin-right: 12px;
    } 
    .delete-btn{
        background-color: #222;
        color: #FCBA03;
        font-weight: bold;
        border: 2px solid #222;
        padding: 10px;
        font-size: 15px;
        margin: 0 auto;
        cursor: pointer;
        transition: .5s;
    }

    .delete-btn:hover{
        background-color: transparent;
        color: #000;
    }
    #lista{
        text-align: start;
    }

</style>