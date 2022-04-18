<template>
    <footer id="footer">
        <p>Your Burguer&copy; 2022</p>
        <p1>By Luan Victor&copy;</p1>
    </footer>
</template>

<script>
export default {
    name: "Footer",
}
</script>

<style scoped>
    #footer {
        background-color: #222;
        height: 225px;
        border-top: 4px solid #111;
        color: #FCBA03;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
    }
</style>
