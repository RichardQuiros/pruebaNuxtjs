<template>
    <div class="container">
     <div class = "card-body">
       <h1>hay un total de:{{resultado.count}} {{$route.params.articulos}}</h1>
       <div class="row">
  <div class="col-4">
    <div class="list-group" id="list-tab" role="tablist">
      <a class="list-group-item list-group-item-action active" id="list-home-list" data-toggle="list" href="#list-home" role="tab" aria-controls="home">Lista</a>
    </div>
  </div>
</div>
     </div>
    </div>
</template>

<script>

import axios from 'axios';
export default {
    
    data(){
        return{
            
            resultado: ''
        }
    }, async created(){
         
        try {
            const res = await axios.get(`https://swapi.dev/api/${this.$route.params.articulos}/`);
            console.log(res.data);
            this.resultado = res.data;
           
        } catch (error) {
            
        }

    }
}
</script>

</script>