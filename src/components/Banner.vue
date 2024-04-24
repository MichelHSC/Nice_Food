<template>
    <div id="main-banner">
        <h1>Make Your Burger</h1>
    </div>
</template>

<script>
export default{
    name: 'Banner'
}
</script>
<style scoped>
#main-banner{
    background-image: url('/public/img/burger.jpg');
    background-repeat: no-repeat;
    border-bottom: 4px solid #11FF00;
    background-position: 0 -250px;
    background-size: cover;
    height: 540px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}
#main-banner h1{
    color: #11FF00;
    text-align: center;
    font-size: 60px;
    background-color: #000;
    padding: 20px 20px;
    border-radius: 0 100px 100px 0;
}
@media (max-width: 768px) {
    #main-banner{
        height: 300px;
        width: 100%;
        background-position: 0;
    }
    #main-banner h1{
        position: relative;
        top: 126px;
    }
    
}
@media (max-width: 900px){
    #main-banner h1{
        font-size: 30px;
    }
}

</style>