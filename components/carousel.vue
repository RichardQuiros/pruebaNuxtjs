
<template>
  <div>
    <b-carousel
      id="carousel-1"
      :interval="2000"
      controls 
      v-model="slide" 
      indicators
      background="#ababab"
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
      fade
    >
    <nuxt-link :to="ActulizarDatoUrlSlides">
      <b-carousel-slide  v-for="(item,index) in slides" :key = index :to="`/swapi/${item.text}`" 
        :text=item.text
        :img-src=item.picture
        img-height="10%"
        img-width="100px" 
      ></b-carousel-slide>
    </nuxt-link>
    </b-carousel>
    

  </div>

</template>
<script>
  export default {
    name: 'carousel',
    props: {slides:{
      default: () =>  [
      { "picture": "https://picsum.photos/1024/480/?image=52","text": "text example1","id": '0',"ruta": "/nosotros" },
      { "picture": "https://i.picsum.photos/id/12/1024/480.jpg","text": "text example2","id": '1',"ruta": "/example1" },
      { "picture": "https://i.picsum.photos/id/23/1024/480.jpg","text":" text example3","id": '2',"ruta": "/exapmle2" }
    ]}
    },
    data() {
      return {
    datoUrl: 0,
    slide: 0,
      }
    },
    computed: {
      ActulizarDatoUrlSlides(){
        return this.slides[this.slide].ruta
      }
    },
  }
</script>