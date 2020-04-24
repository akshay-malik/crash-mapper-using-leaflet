<template>
<b-container fluid> 
    <b-row>
      <b-col id="sidebar" cols="4" >
        <Sidebar /> 
      </b-col>
      <b-col >
        <Webmap />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import Webmap from './components/Webmap.vue'
import Sidebar from './components/Sidebar.vue'
import BootstrapVue from 'bootstrap-vue'

import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'
import Vue from 'vue'
Vue.use(BootstrapVue)

export default {
  name: 'App',
  components: {
    Webmap, Sidebar
  }
}
</script>

<style>

  #map { 
    height: 95vh;
    margin: 1.3em ;
    border: 6px double rgba(28,110,164,0.12);
    border-radius: 7px 7px 7px 7px;

    }

    #sidebar {
    overflow: scroll;
    margin: 1em 0em 1em 1em;
    padding-bottom: 0; 
    border: 6px double rgba(28,110,164,0.12);
    border-radius: 7px 7px 7px 7px;
    height: 95vh;
  }  

  .col {
    margin: 0;
    padding: 0;
  }
</style>
