<template>
  <div class="hello">
    <h1>{{ title }}</h1>
    <h2>{{ tagline }}</h2>

  </div>
</template>

<script>
export default {
  name: 'github',
  data () {
    return {
      title: 'Github Vue',
      tagline: 'Simple Vue JS app to display your Github Commits'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
