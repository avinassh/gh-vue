<template>
  <div>
    <section class="container">
      <div class="username-label has-text-left">Enter the username</div>
      <input v-model="username" @keyup.enter="update" class="input" type="text"/>
    </section>
    <section>
      <div class="container table-container">
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
          <div class="has-text-centered is-full-width" v-if="!commits.length && fetching">
            <i class="fa fa-3x fa fa-circle-o-notch fa-spin"></i>
          </div>
          <div class="has-text-centered is-full-width" v-if="!commits.length && !fetching">
            <div>
              <i class="fa fa-3x fa-frown-o" aria-hidden="true"></i>
            </div>
            <div>Nothing to show here.</div>
          </div>
      </div>
    </section>
  </div>
</template>

<script>
  export default {
    name: 'github',
    data () {
      return {
        username: 'avinassh',
        commits: null,
        fetching: true
      }
    },

    created: function () {
      this.update()
    },

    methods: {
      update: function () {
        var xhr = new XMLHttpRequest()
        var self = this
        self.fetching = true
        self.commits = []
        xhr.open('GET', 'https://api.github.com/users/' + self.username + '/events/public')
        xhr.onload = function () {
          self.fetching = false
          JSON.parse(xhr.responseText).forEach(function (eventItem) {
            if (eventItem.type === 'PushEvent') {
              eventItem.payload.commits.forEach(function (commitItem) {
                var commit = {}
                commit.repo = eventItem.repo
                commit.sha = commitItem.sha
                commit.url = commitItem.url.replace('api', 'www').replace('/repos', '').replace('commits', 'commit')
                commit.msg = commitItem.message
                self.commits.push(commit)
              })
            }
          })
        }
        xhr.send()
      }
    }
  }
</script>

<style>
  .table-container {
    margin-top: 20px;
  }
  a {
    color: #097af1;
  }
  .username-label {
    margin-bottom: 5px;
  }
  .fa-3x {
    font-size: 3em !important;
  }
</style>
