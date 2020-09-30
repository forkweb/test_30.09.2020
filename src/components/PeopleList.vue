<template>
  <div class="pople">

    <input type="text" v-model="inputSearch" autofocus>

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
      inputSearch: ''
    }
  },
  computed: {
    // filteredItems() {
    //   return this.peoples.filter(people => {
    //      return people.type.toLowerCase().indexOf(this.inputSearch.toLowerCase()) > -1 || people.name.toLowerCase().indexOf(this.inputSearch.toLowerCase()) > -1
    //   })
    // }
    // filteredItems()  {
    //   let inputSearch = this.inputSearch.trim();
      
    //   if(inputSearch) {
    //     inputSearch = inputSearch.toLowerCase();
    //     return this.peoples.filter(people => people.toLowerCase().includes(inputSearch))
    //   }

    //   return this.peoples
    // }
    filteredItems(){
      return this.peoples.filter(people => {
        return people.name.toLowerCase().includes(this.inputSearch.toLowerCase())
      })
    }
    
  },
  methods: {
    GetPoples() {
      axios.get(`${baseUrl}/api/people/`).then(response => (this.peoples = response.data.results));
    }
  },
  mounted(){
    this.GetPoples();
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
