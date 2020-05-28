<template>
    <div class="b-container">
     <b-navbar toggleable type="dark" variant="dark">
    <b-navbar-brand to="/" ><logo/>Nuxt practice by Richard Quiros</b-navbar-brand>
 
    <b-navbar-toggle target="navbar-toggle-collapse">
      <template v-slot:default="{ expanded }">
        <div v-if="expanded" ><b-icon-chevron-double-up></b-icon-chevron-double-up></div>
        <div v-else ><b-icon-chevron-double-down></b-icon-chevron-double-down></div>
      </template>
    </b-navbar-toggle>

    <b-collapse id="navbar-toggle-collapse" is-nav>
      <b-navbar-nav class="ml-auto">
        <b-nav-item to="/">Home</b-nav-item>
        <b-nav-item to="/swapi">Swapi</b-nav-item>
        <b-nav-item to="#" disabled>StarWars Game</b-nav-item>
        <b-nav-item to="/nosotros">Nosotros</b-nav-item>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
    </div>
</template>

<script>
import logo from '~/components/logo.vue'
import { BootstrapVue, IconsPlugin, BIconArrowUp,BIconChevronDoubleDown,BIconChevronDoubleUp } from 'bootstrap-vue'
export default {
  components:{
       logo,
        BIconArrowUp,
        BIconChevronDoubleUp,
        BIconChevronDoubleDown
        }
}
</script>