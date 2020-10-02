<template>
  <div class="pople">

    <input type="text" v-model="inputSearch" autofocus>

    <br>

    <button v-on:click="SortName">По имени</button>
    <button v-on:click="SortDate">По дате</button>
    <button v-on:click="SortMass">По весу</button>
    
 

    <div class="item_pople" v-for="(people, index) in filteredItems" v-bind:key="index">

      {{people.name}}
      {{index}}

    </div>

  </div>
</template>


<script>

import axios from 'axios';

const baseUrl = 'https://swapi.dev';

export default {
  name: 'PeopleList',
  data() {
    return {
      peoples: [],
      inputSearch: '',
      search: { filter: null, text: "" },
    }
  },
  computed: {
    filteredItems(){
      return this.peoples.filter(people => {
        return people.name.toLowerCase().includes(this.inputSearch.toLowerCase())
      });
    }
    
  },
  methods: {
    GetPoples() {
      axios.get(`${baseUrl}/api/people/`).then(response => (this.peoples = response.data.results));
    },
    SortName() {
      function compare(a, b) {
        if (a.name < b.name)
          return -1;
        if (a.name > b.name)
          return 1;
        return 0;
      }
      return this.peoples.sort(compare);
    },
    SortDate(){

    },
    SortMass(){
      function compare(a, b) {
        if (a.mass < b.mass)
          return -1;
        if (a.mass > b.mass)
          return 1;
        return 0;
      }
      return this.peoples.sort(compare);
    }
  },
  mounted(){
    this.GetPoples();
    this.SortName();
  }
}
</script>


<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
