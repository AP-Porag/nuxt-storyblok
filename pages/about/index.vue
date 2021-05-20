<template>
  <section id="about-page">
    <div class="container text-center">
      <h1>{{title}}</h1>
      <p class="about_content">{{content}}</p>
    </div>
  </section>
</template>

<script>
export default {
  name: "index",
  asyncData(ctx) {
    return ctx.app.$storyapi.get('cdn/stories/about',{
      version:'draft'
    }).then(res => {
      return{
        title: res.data.story.content.title,
        content: res.data.story.content.content,
      }
    })
  }
}
</script>

<style scoped>
.about_content{
  white-space: pre-line;
}
</style>
