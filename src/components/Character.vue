<template>
  <div>

    <div class="flex-container">
      <div class="flex" v-for="char in character">
        <h3>
          {{char.name}}
        </h3>
        <p>
          {{char.description}}
        </p>
      

      </div>

      <div class="flex2">
        <img :src="url" alt="" class="char-img">

      </div>
    </div>
    <router-link to="/">
      <button type="button" name="button" class="btn-back">Back</button>

    </router-link>

  </div>
</template>

<script >
import { public_key } from '../marvel';
import axios from 'axios'
export default {
    name: 'character',
    data() {
      return {
        character: [],
        url:'',
        size:'standard_large.jpg',
      }
    },
    mounted() {
      this.getCharacter()
    },
    methods: {
      getCharacter: function() {
        var characterId = this.$route.params.id
        axios.get(`http://gateway.marvel.com/v1/public/characters/${characterId}?apikey=${public_key}`)
        .then((result) =>{
          console.log(result)
          result.data.data.results.forEach((item) => {
            this.character.push(item)
            this.url = `${item.thumbnail.path}/${this.size}`
          });
        })
        .catch((error) =>{
          console.log(error)
        })
      }
    }
}
</script>


<style>
.flex-container {
  margin: 100px;
  display: flex;
  align-items: center;
  justify-content: center;

}
.flex {
  flex: 50%;
  text-align: right;
}

.flex2 {
  flex: 50%;
}
.char-img {
  width: 50%;
  border-radius: 10px;

}
.btn-back {
  width: 200px;
  padding: 15px;
  border-radius: 25px;
  background-color: transparent;
  font-size: 20px;
  margin-bottom: 100px;
  cursor: pointer;

}
</style>