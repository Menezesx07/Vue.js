<template>
  <div class="home">
  
        <div id="Container-Cadastro">
          <Cadastro/>
          <Divisor/>
          <Tabela/>
        </div>
  </div>
</template>

<script>

import Cadastro from "../components/Cadastro.vue";
import Tabela from "@/components/Tabela.vue";
import Divisor from "@/components/Divisor.vue";

export default {
    components: { Cadastro, Tabela, Divisor }
}
</script>

<style>

#Container-Cadastro{
  display: flex;
  flex-direction: row;
  
}

</style>