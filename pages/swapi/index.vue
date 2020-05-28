<template>
    <div  v-if="verf" class=" container mt-2">
        <div class="row  d-flex justify-content-center">
    <div class="row bg-dark d-flex justify-content-center">
        <img class="img-fluid" src="http://pngimg.com/uploads/star_wars_logo/star_wars_logo_PNG42.png" 
        width="200" height="100" alt="star wars">
            <carousel :slides='slides'/>

            <b-button :to="`/swapi/${item.id}`" class=" col btn-sm mt-5 mb-5 ml-2 mr-2 text-capitalize text-center   " pill variant="outline-warning"
    v-for="(item,index) in slides" :key="index" style="font-size:2vw">
        {{item.id}}
    </b-button>
       </div>
         
        

        <div  class="container mt-5 mb-5 p-5 bg-dark text-white row  d-flex justify-content-start">
           <a href="https://swapi.dev/"> <h1 style="font-size:4vw" class="text-warning font-weight-bold">SWAPI:the star wars API   
            </h1></a>
          <div class="row">
            <h2 style="font-size:3vw">What is this?</h2>
        <h5 style="font-size:2vw" ><p>The Star Wars API is the world's first quantified and programmatically-formatted set of Star Wars data.
                                      After hours of watching films and trawling through content online, we present to you all the People, Films,
                                       Species, Starships, Vehicles and Planets from Star Wars.
                                      We've formatted this data in JSON and exposed it to you in a RESTish implementation that allows you to programmatically collect and measure the data.</p></h5>
        </div>
        </div>
    </div>
    </div>
  
</template>

<script>
import axios from 'axios'
import carousel from '~/components/carousel.vue'
export default {
    components:{
       carousel
    },
    data(){
        return{
           tipos: [],
           datosSlides: [{picture: 'https://wallpaperplay.com/walls/full/2/a/8/124152.jpg'},
           {picture: 'https://wallpaperplay.com/walls/full/7/e/8/124156.jpg'},
           {picture: 'https://wallpaperplay.com/walls/full/a/0/5/124143.jpg'},
           {picture: 'https://wallpapercave.com/wp/wp4959346.jpg'},
           {picture: 'https://wallpaperplay.com/walls/full/1/6/3/124137.jpg'},
           {picture: 'https://wallpaperplay.com/walls/full/d/2/2/124140.jpg'}],
           slides: [],
           verf: false
           
        }
    },  methods:{
        async init () {
        const entradasDB = await axios.get('https://swapi.dev/api/');
        const entradasDatos = Object.keys(entradasDB.data)
         let i = 0
         let entrada= []
        await entradasDatos.forEach(element => {
          entrada.push({picture: this.datosSlides[i].picture,text: entradasDatos[i],id: entradasDatos[i],ruta: '/swapi/'+element})
          i++
        })
        console.log(entrada)
        this.slides = entrada
        this.verf=true
      }
    },
created (){
        
         this.init ()
    },
    computed:{
        updateSlides(){
            if(this.slides != this.verf){
                this.verf = true
                return verf
            }
            else{return verf}

        }
    }
}
</script>
    