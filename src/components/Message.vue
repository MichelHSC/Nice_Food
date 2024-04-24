<template>
    <div class="message-container">
        <p> {{ msg }} </p>
    </div>
</template>
<script>
export default{
    name: 'Message',
    props:{
        msg: String
    }
}
</script>

<style scoped>
.message-container{
    color: #000;
    background-color: #11ff00;
    border: 2px solid #0ead02;
    border-radius: 5px;
    padding: 10px;
    max-width: 400px;
    margin: 30px auto;
}
.message-container p{
    font-weight: bold;
    text-align: center;
}
</style>