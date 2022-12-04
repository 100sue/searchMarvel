<template>
  <div>
    <h1>characters vue</h1>

    <ul>
      <li v-for="character in characters">
        <router-link :to="{name:'character', params: { id: character.id}}">{{character.name}}</router-link>
      
      </li>


    </ul>


  </div>
</template>

<style >

</style>

<script >
import {public_key, secret_key} from '../marvel';
import axios from 'axios';

export default {
    name: 'Characters',
    data() {
      return {
        characters: []
      }

    },

    mounted () {
      this.getCharacters()

    },

/*obtention des data avec key, puis boucle pr les classer */

    methods: {
      getCharacters: function() {
        axios.get(`http://gateway.marvel.com/v1/public/characters?apikey=${public_key}`)
          .then ((result) => {
        
            result.data.data.results.forEach((item)=>{
              console.log(item)

              this.characters.push(item)
            })
          })
          .catch((error)=> {
            console.log(error)
          })
        }
    }
}

</script>