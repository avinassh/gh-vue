<template>
  <div>
  <section class="hero">
    <div class="hero-body">
      <div class="container">
        <h1 class="title">
          {{ title }}
        </h1>
        <h2 class="subtitle">
          {{ tagline }}
        </h2>
      </div>
    </div>
  </section>
  <section>
    <div class="container">
      <table class="table">
        <thead>
        <tr>
          <th>Repo</th>
          <th>Commit</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="commit in commits">
          <td><a :href="commit.repo.url">{{ commit.repo.name }}</a></td>
          <td><a :title="commit.sha" :href="commit.url">{{ commit.msg }}</a></td>
        </tr>
        </tbody>
      </table>
    </div>
  </section>
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
      self.commits = []
      xhr.open('GET', 'https://api.github.com/users/avinassh/events/public')
      xhr.onload = function () {
        JSON.parse(xhr.responseText).forEach(function (eventItem) {
          if (eventItem.type === 'PushEvent') {
            var commit = {}
            commit.repo = eventItem.repo
            eventItem.payload.commits.forEach(function (commitItem) {
              commit.sha = commitItem.sha
              commit.url = commitItem.url
              commit.msg = commitItem.message
            })
            self.commits.push(commit)
          }
        })
      }
      xhr.send()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
