<template>
  <div class="b-container">
  <navbar/>
  <breadcrumb/>
    <nuxt/>
    <piePagina/>
    
  </div>
</template>

<script>
import navbar from '~/components/navbar.vue'
import piePagina from '~/components/piePagina.vue'
import breadcrumb from '~/components/breadcrumb.vue'
export default {
  components:{

       navbar,
       piePagina,
       breadcrumb
    },
}
</script>