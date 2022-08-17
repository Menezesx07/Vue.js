<template>
    <div id="Header">
        <div id="Titulo-Container">
            <img :src="logo" :alt="alt" id="logo">
            <h1>Agenda</h1>
        </div>
        
        <nav>
            <router-link to="/">Home</router-link> |
            <router-link to="/about">About</router-link>
        </nav>
    </div>
</template>

<script>
export default {
    name: "Header",
    data(){
        return {
            logo: "/img/agenda.png",
            Alt: "Agenda"
        }
    }
}
</script>

<style scoped>

#Header{
    background-color: rgb(24, 95, 119);
    display: flex;
    align-items: center;
    height: 70px;
}

#Titulo-Container{
    display: flex;
    align-items: center;
    position: absolute;
    left: 5%;
}

h1 {
    margin-left: 30px;
    color: white;
}

img{
    height: 50px;
}

nav{
    position: absolute;
    right: 5%;
}
 
nav a{
    margin: 10px;
    text-decoration: none;
    color: white;
    cursor: pointer;
    transition: 0.5s;
}

nav a:hover {
    color: black;
}



</style>