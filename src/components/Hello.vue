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
  </div>
</template>
<script>
  export default {
    name: 'hello',
    data () {
      return {
        title: 'Github Vue',
        tagline: 'Simple Vue JS app to display your latest Github Commits'
      }
    }
  }
</script>
