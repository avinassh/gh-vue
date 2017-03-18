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
      tagline: 'Simple Vue JS app to display your Github Commits',
      commits: null
    }
  },

  created: function () {
    this.update()
  },

  methods: {
    update: function () {
      var xhr = new XMLHttpRequest()
      var self = this
      xhr.open('GET', 'https://api.github.com/users/avinassh/events/public')
      xhr.onload = function () {
        self.commits = JSON.parse(xhr.responseText)
        console.log(self.commits)
      }
      xhr.send()
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
