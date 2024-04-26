<template>
    <div id="nav">
        <router-link to="/" id="logo_url" @click="logar">
            <img :src="logo" :alt="alt" id="logo">
        </router-link>
        <router-link to="/" id="txt-nav">Home</router-link>
        <router-link v-show="logOn" to="/pedidos" id="txt-nav">Pedidos</router-link>
    </div>
</template>
<script>
export default{
    name: "Navbar",
    props:['logo','alt'],
    data(){
        return{
            logOn: false
        }
    },
    methods:{
        logar(){
            this.logOn = !this.logOn
        }
    }

}
</script>
<style scoped>

</style>

<style scoped>
#nav{
    background-color: #000;
    border-bottom: 4px solid #11FF00;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    width: 100%;
}
#nav #logo_url{
    margin: auto;
    margin-left: 0;
    
}

#logo{
    width: 40px;
    height: 40px;
}

#nav a {
    color: #11FF00;
    text-decoration: none;
    margin: 12px;
    transition: .5s;
}

#nav a:hover{
    color: #FFF;
}
#txt-nav{
    font-weight: Bold;
    font-size: 18px;
}

</style>