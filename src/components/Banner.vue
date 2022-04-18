<template>
    <div id="main-banner">
        
    </div>
</template>

<script>
export default {
    name: "Banner",
}
</script>

<style scoped>
    #main-banner {
        background-image: url("/public/img/burger.jpg");
        background-position: 0 -100px;
        background-size: cover;
        height: 600px;
        width: 100%;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        filter: drop-shadow(0px 4px 4px rgba(0, 0, 0, 0.25));
        box-shadow: inset 0px 4px 4px rgba(0, 0, 0, 0.25);
    }

    #main-banner h1{
        color: #FFF;
        text-align: center;
        font-size: 60px;
        background-color: #222;
        padding: 20px 40px;
    }
</style>
