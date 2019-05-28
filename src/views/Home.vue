<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App + Store Structured"/>
    <br>
    <h2>👑Example request using JSONPlaceholder👑</h2>
    <input type="text" v-model="search" placeholder="search ...">
    <div>
      <div v-if="isLoading">
        Loading ...
      </div>
      <div v-else>
        <div v-for="content in filteredDataObj" :key="content.id">
          <li>{{content.title}}</li>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import {mapState , mapGetters} from 'vuex';
  import HelloWorld from "@/components/HelloWorld.vue";
  import store from '../store/store.js';

  export default {
    name: "home",
    components: {HelloWorld},
    data(){
      return{
        search: ''
      }
    },
    computed:{
      ...mapState(['data' , 'isLoading']),
      ...mapGetters(['FILTER_SPESIFIC_DATA']),
      filteredDataObj(){
        return this.FILTER_SPESIFIC_DATA(this.search)
      }
    },
    created(){
      store.dispatch('GET_DATA')
    }
  };
</script>

