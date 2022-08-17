<template>
    <div id="Footer">
        <p>Agenda Vue.js- Rafael Henrique  &copy; 2022</p>
    </div>
</template>

<script>
export default {
    name: "Footer"
}
</script>

<style scoped>

#Footer{
    background-color: rgb(24, 95, 119);
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    height:60px;
    width: 100%;
    position: absolute;  /* Fixar o rodapé no fim da pagina */
    bottom: 0;           /* Fixar o rodapé no fim da pagina */
}

</style>