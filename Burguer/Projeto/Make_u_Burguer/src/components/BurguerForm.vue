<template>
    
     <form id="burger-form" @submit="createBurger"> <!-- quando usar o botão do formulario, vai usar o metodo de createBurger-->

        <div class="input-container"> <!-- Nome do Cliente -->
            <label for="nome"> Nome do cliente </label>
            <input type="text" id="nome" name="nome" v-model="nome" placeholder="Digite seu nome">
        </div>

        <div class="input-container"> <!-- Escolha do pão -->
            <label for="pao"> Escolha o pão: </label>
            <select name="pao" id="pao" v-model="pao">
                <option value="">Selecione o seu pão</option>
                <!-- trabalhando com o metodo getIngredientes()-->
                <option v-for="pao in paes" :key="pao.id" value="pao.tipo">{{pao.tipo}}</option> 
            </select>
        </div>

        <div class="input-container"> <!-- Escolha da carne-->
            <label for="carne"> Escolha a carne: </label>
            <select name="carne" id="carne" v-model="carne">
                <option value="">Selecione a carne</option>
                <!-- trabalhando com o metodo getIngredientes()-->
                <option v-for="carne in carnes" :key="carne.id" value="carne.tipo">{{carne.tipo}}</option> 
            </select>
        </div>

        <div id="opcionais-container" class="input-container"> <!-- Escolha dos opcionais -->
            <label for="opcionais"> Selecione os opcionais: </label>
            <!-- trabalhando com o metodo getIngredientes()-->
            <div class="checkbox-container" v-for="opcional in opcionaisdata" :key="opcional.id">
               <input type="checkbox" name="opcionais" v-model="opcionais" :value="opcional.tipo">
               <span>{{opcional.tipo}}</span>
                
            </div> 
        </div>

        <div class="input-container">  <!-- Botão enviar -->
           <input type="submit" class="submit-btn" value="Criar meu Burger!">
             
        </div>
     </form>
</template>

<script>
export default {
    name: "burguerFrom",
    data(){
        return{
            paes: null,    
            carnes: null,
            opcionaisdata: null,
            nome: null,
            pao: null, 
            carne: null,
            opcionais: [],
            msg: null
        }    
    }, 
    methods: {
        async getIngredientes(){
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();
           
            this.paes = data.paes;   /*requisições para buscar os ingredientes do servidor para o selecionar*/
            this.carnes = data.carnes;
            this.opcionaisdata = data.opcionais;

        },
        async createBurger(e){
            e.preventDefault(); //para não recarregar a pagina ao clicar no botão
            const data = {
                nome: this.nome,
                carne: this.carne,
                pao: this.pao,
                opcionais: Array.from(this.opcionais),
                status: "Solicitado"
            }

            const dataJason = JSON.stringify(data);
            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: { "Content-type": "application/json" },
                body: dataJson
            });

            const res = await req.json();
            
        }

    },
    mounted(){
        this.getIngredientes();
    }
}
</script>

<style>

#burger-form{
    max-width: 400px;
    margin: 0 auto;
}

.input-container{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
}

label {
    font-weight: bold;
    margin-bottom: 15px;
    color: #222;
    padding: 5px 10px;
    border-left: 4px solid orange;
}

input,select{
    padding: 5px 10px;
    width: 300px;
}

#opcionais-container{
    display: flex;
    flex-direction:row;
    flex-wrap: wrap;
}

#opcionais-title{
    width: 100%;
}

.checkbox-container {
    display: flex;
    align-items:flex-start;
    width: 50%;
    margin-bottom: 20px;
}

.checkbox-container span,
.checkbox-container input {
    width: auto;
}
 

.checkbox-container span {
    margin-left: 6px;
    font-weight: bold;
}

.submit-btn{
    background-color: #222;
    color: orange;
    font-weight: bold;
    border: 2px solid #222;
    font-size: 16px;
    cursor:pointer;
    transition: 0.5s;
}

.submit-btn:hover {
    background: transparent;
    color: #222;
}




</style>