<template>
    <div id="Cadastro">
        <form class="Input-Container" @submit="createCadastro">
            
            <label>Nome</label>
            <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite o nome" 
             minlength="5" maxlength="20">

            <label>Telefone</label>
            <input type="text" id="telefone" name="telefone" v-model="telefone" placeholder="Digite o nome" 
             minlength="5" maxlength="20">

            <label>E-Mail</label>
            <input type="text" id="email" name="email" v-model="email" placeholder="Digite o nome" 
             minlength="5" maxlength="20">

             <input type="submit" id="submit-btn" value="Cadastrar">


        </form>
        
    </div>
</template>

<script>
export default {
    name: "Cadastro",
    methods: {
        async createCadastro (e) {
            e.preventDefault(); //segurar o reload da pagina
            const data = {
                nome: this.nome, //dando get nos campos e atribuindo ao data
                telefone: this.telefone,
                email: this.email
            }; 

           

            const dataJson = JSON.stringify(data); //convertendo o data para json

            console.log(dataJson);

              const req = await fetch("http://localhost:8090/contato", {
              method: "POST",
              headers: { "Content-Type": "application/json" },
              body: dataJson
            });

            //limpando os campos do formulario
           // document.querySelector('form').reset()
           
        }
    }


}
</script>

<style scoped>

#Cadastro{
    background-color: lightgrey;
    display: flex;
    justify-content: center;
    width: 300px;
    height: 450px;
    margin-top: 30px;
    margin-left: 30px;
}

.Input-Container{
    display: flex;
    flex-direction: column;
}

label {
    font-weight: bold;
    margin-top: 30px;
    margin-bottom: 10px;
    color: grey;
    padding: 5px 10px;
    font-size: 24px;
    border-left: 4px solid rgb(24, 95, 119);
}

input{
    padding: 5px 10px;
    width: 200px;
    height: 40px;
    border-radius: 3px;
    border-style: solid;
}

#submit-btn {
   background-color: rgb(24, 95, 119);
   color: white;
   font-size: 18px;
   border-style: none;
   font-weight: bold;
   margin-top: 30px;
   width: 200px;
   height: 40px;
   cursor: pointer;
   transition: 0.5s;   
}

#submit-btn:hover {
    background: transparent;
    color: gray;
    border: 2px solid rgb(24, 95, 119);
}

</style>