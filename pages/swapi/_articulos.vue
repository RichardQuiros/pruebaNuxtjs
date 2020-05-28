<template>
    <div   v-if="verf" class="container text-left   mt-5 bg-dark p-5">
        <div class="col">
       <h1 class="text-capitalize text-warning row ">{{resultado.count}} {{$route.params.articulos}}</h1>
       <div class="row">
       <TableSwapiResult v-if="$route.params.articulos==='films'" :items='items' :fields='fieldFilms'/>
       <TableSwapiResult v-else-if="$route.params.articulos==='people'" :items='items' :fields='fieldPeople'/>
       <TableSwapiResult v-else-if="$route.params.articulos==='species'" :items='items' :fields='fieldSpecies'/>
       <TableSwapiResult v-else-if="$route.params.articulos==='vehicles'" :items='items' :fields='fieldVehicles'/>
       <TableSwapiResult v-else-if="$route.params.articulos==='planets'" :items='items' :fields='fieldPlanets'/>
       <TableSwapiResult v-else-if="$route.params.articulos==='vehicles'" :items='items' :fields='fieldFilms'/>
       <TableSwapiResult v-else-if="$route.params.articulos==='starships'" :items='items' :fields='fieldVehicles'/>
       </div>
    </div>
    </div>
</template>

<script>

import axios from 'axios';
import TableSwapiResult from '~/components/TableSwapiResult.vue'
export default {
    components: {TableSwapiResult},
    data(){
        return{
            verf: false,
            resultado: [],
            items: [],
            fieldFilms: [{key: 'title', label: 'Title', sortable: true, sortDirection: 'desc' },
            {key: 'director', label: 'Director', sortable: true, sortDirection: 'desc' },
            {key: 'producer', label: 'Producer', sortable: true, sortDirection: 'desc' },
            {key: 'release_date', label: 'Date', sortable: true, sortDirection: 'desc' },
            {key: 'episode_id', label: 'Episode', sortable: true, sortDirection: 'desc' },
            { key: 'actions', label: 'Actions' }],
            fieldPeople: [{key: 'name', label: 'Name', sortable: true, sortDirection: 'desc' },
            {key: 'gender', label: 'Gender', sortable: true, sortDirection: 'desc' },
            {key: 'birth_year', label: 'Birth Year', sortable: true, sortDirection: 'desc' },
            {key: 'created', label: 'Created', sortable: true, sortDirection: 'desc' },
            { key: 'actions', label: 'Actions' }],
            fieldSpecies: [{key: 'name', label: 'Name', sortable: true, sortDirection: 'desc' },
            {key: 'designation', label: 'Designation', sortable: true, sortDirection: 'desc' },
            {key: 'classification', label: 'Classification', sortable: true, sortDirection: 'desc' },
            {key: 'language', label: 'Language', sortable: true, sortDirection: 'desc' },
            { key: 'actions', label: 'Actions' }],
            fieldVehicles: [{key: 'name', label: 'Name', sortable: true, sortDirection: 'desc' },
            {key: 'model', label: 'Model', sortable: true, sortDirection: 'desc' },
            {key: 'passengers', label: 'Passengers', sortable: true, sortDirection: 'desc' },
            {key: 'cost_in_credits', label: 'Cost in credits', sortable: true, sortDirection: 'desc' },
            { key: 'actions', label: 'Actions' }],
            fieldPlanets: [{key: 'name', label: 'Name', sortable: true, sortDirection: 'desc' },
            {key: 'climate', label: 'Climate', sortable: true, sortDirection: 'desc' },
            {key: 'terrain', label: 'Terrain', sortable: true, sortDirection: 'desc' },
            {key: 'population', label: 'Population', sortable: true, sortDirection: 'desc' },
            { key: 'actions', label: 'Actions' }], 
        }
    },
    methods:{
         async init(){
             let next 
             let entrada = []
             let ruta = `https://swapi.dev/api/${this.$route.params.articulos}/`
             let res = []
           try {
             do{
              res = await axios.get(ruta);
              entrada.push(...res.data.results)
              next = res.data.next
              ruta = res.data.next 
            }while(next)
             this.resultado = res.data;
             this.items = entrada
             this.verf = true
          //  console.log(this.items)
        } catch (error) {
        }
          }
    }, 
    created(){
         
        this.init()

    },
    mounted(){
    this.$emit('Example',"hello world")
    }
}
</script>

</script>