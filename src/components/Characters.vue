<template>
<div>

  <div class="card-container">
    <div class="card" v-for="character in characters">
      <h3>{{character.name}}</h3>
      <router-link :to="{name:'character', params: { id: character.id}}">
        <button type="button" name="button" class="btn-view">View</button>
      
      </router-link>
    </div>
   
  </div>

</div>
  

</template>


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

<style >
.card-container {
  margin-left: 310px;
  display: grid;
  grid-template-columns: 200px 200px 200px;
  grid-gap: 10px
}
.card {
  text-align: center;
  background-color: #777;
  min-height: 200px;
  max-width: 200px;
}
.card h3 {
  color: #fff;
}
.btn-view {
  padding: 10px;
  margin-top: 50px;
  border-radius: 15px;
  width: 120px;
  background-color: transparent;
  color: #fff;
  font-size: 12px;
  font-weight: bold;
  cursor: pointer;
}
</style>