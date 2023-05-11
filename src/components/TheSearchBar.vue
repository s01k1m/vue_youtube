<template>
  <div class="hello">
    <input v-on:keyup.enter='onEmit'>
  </div>
</template>

<script>

export default {
  name: 'TheSearchBar',
  data() {
    return {
      search: null
    }
  },
  props: {

  },
  methods: {
    onEmit(event) {
      this.$emit('search', event.target.value)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
