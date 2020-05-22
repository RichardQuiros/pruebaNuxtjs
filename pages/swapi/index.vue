<template>
    <div class="container mt-5">
        <div class="row">
    <div class="col-md-3" 
    v-for="(item,index) in tipos" :key="index">
        <h2><nuxt-link :to="`/swapi/${item.id}`">{{item.title}}</nuxt-link></h2> 
    </div>
    </div> 
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return{
           tipos: [{title: 'Peliculas',id: 'films'},{title: 'Personajes',id: 'people'},{title: 'Planetas',id: 'planets'},
           {title: 'Especies',id: 'species'},{title: 'Naves Espaciales',id: 'starships'},{title: 'Vehiculos',id: 'vehicles'},]
        }
    },
    async created(){
        try {
             const res = await axios.get('https://swapi.dev/api/')
        this.tipos = res.data;
        console.log(res.data);
        } catch (error) {
            //console.log(error);
        }
       
    }
}
</script>