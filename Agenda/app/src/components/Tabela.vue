<template>
    <div id="Tabela">
        <div class="tabela-container">

                <div class="tabela-headers">
                    <div id="cadastro-header">
                        <div>Nome</div>
                        <div>Telefone</div>
                        <div>Email</div>
                        <div class="alterar">Alterar</div>
                        <div class="deletar">Excluir</div>
                    </div>

                    <div id="cadastro-rows">

                        <div class="cadastro-row" v-for="cadastro in cadastro" :key="cadastro.id">
                            <div>{{cadastro.nome}}</div>
                            <div>{{cadastro.telefone}}</div>
                            <div>{{cadastro.email}}</div>
                            <button id="btn-alterar" class="btn" @click="alterarContato(cadastro.id)">A</button>
                            <button id="btn-deletar" class="btn" @click="deleteContato(cadastro.id)">X</button>  
                        </div>

                    </div>
                
                </div>

            </div>
    </div>
</template>

<script>
export default {
    name: "Tabela",
     data() {
        return {
            nome: null,
            telefone: null,
            email: null,
            id: null,
            cadastro: null
        };
    },
    methods: {
        async getCadastro() {
            const req = await fetch("http://localhost:8090/contato")
            const data = await req.json();
            this.cadastro = data; //cadastro no qual foi associado esta no v-for do html
        }

    },
        async deleteContato(id) {
            
            //transformando o id que vinha cru, em um data para ser passado
            //como parametro no Servidor 
            this.id = id
             const data = {
                id: this.id
            };

            const dataJson = JSON.stringify(data);
            console.log(dataJson)
           
            const req = await fetch(`http://localhost:8090/contato/`, {
                method: "DELETE",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            });
            
            this.getCadastro();
            
    },
    mounted() {
        this.getCadastro();
      
    }
}
</script>

<style scoped>

.tabela-container{
   display: flex;
   margin-top: 30px;
   height: 450px;
   max-width: 900px;
   background-color: lightgray;
  
}

 .tabela-headers{
  width: auto; 
  height:inherit; /*herdar altura */
  overflow:auto; /*ativar o scroll*/
 }

 /*scroll*/

.divTable::-webkit-scrollbar {
  width: 7px;
  background-color: whitesmoke; 
}
.tabela-headers::-webkit-scrollbar {
  width: 15px;
  background-color: whitesmoke; 
}

/*scroll*/

#cadastro-header,
#cadastro-rows,
.cadastro-row{
    display: flex;
    flex-wrap: wrap;
}

#cadastro-header {
    font-weight: bold;
    padding: 12px;
    background-color: rgb(24, 95, 119);
    color: white;
}


#cadastro-header div,
.cadastro-row div {
    width: 200px;
}

.cadastro-row {
    width: 100%;
    padding: 12px;
    border-bottom: 1px solid lightseagreen; 
}

#cadastro-rows {
    display: flex;
    flex-direction: column-reverse;
}

.alterar {
    width: 70px !important;
    margin-left: 70px;
}

.deletar{
    width: 70px !important;
}

#btn-deletar {
    width: 30px;
    height: 23px;
    margin-left: 130px;
    background-color: rgb(240, 51, 51);
    transition: .5s;  
    cursor: pointer;
    border-style: none;
    border-radius: 5px;
}

#btn-deletar:hover {
    background-color: transparent;
}




</style>