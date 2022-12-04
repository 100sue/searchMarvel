<template>
  <div>
    <h3>Hello this is character.vue</h3>
    <p>{{ this.$route.params.id}}</p>
  </div>
</template>

<script >
export default {
    name: 'character'
}

</script>


<style>

</style>