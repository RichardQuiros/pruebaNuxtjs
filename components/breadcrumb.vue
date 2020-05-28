<template>
    <div class="bg-dark">
   <b-breadcrumb class="bg-dark" >  
    <b-breadcrumb-item v-for="(item,index) in ruta" :key="index" :to="item.ruta">{{item.text}}
    </b-breadcrumb-item>
  </b-breadcrumb>
  </div>
</template>

<script>
export default {
    data(){
  return{
 ruta:  [],
  }
},
methods:{
   getRoute(){
     this.ruta = []
     let verf = true
    let  rutaArray = this.$route.path.split("/")
    rutaArray.forEach(element => { 
      if(verf){
        this.ruta.push({text: 'home',ruta: '/'})
        verf = false
      }
      else{
        this.ruta.push({text: element,ruta: '/'+element})
      }
    });
   console.log('la ruta es e: '+rutaArray)
  }
},
created(){
  this.getRoute()
}
}
</script>