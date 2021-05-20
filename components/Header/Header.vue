<template>
  <!-- Header Section Begin -->
  <header class="header">
    <TopBar/>
    <NavBar/>
  </header>
  <!-- Header Section End -->

</template>

<script>
import TopBar from "~/components/Header/TopBar";
import NavBar from "~/components/Header/NavBar";
export default {
  name: "Header",
  components:{
    TopBar,
    NavBar
  },
  asyncData(ctx) {
    return ctx.app.$storyapi.get('cdn/stories',{
      version:'draft',
      starts_with:'category/'
    }).then(res => {
      console.log(res)
      return {
        categories : res.data.stories.map(category => {
          return{
            id:category.id,
            slug:category.slug,
            title:category.content.title,
            thumbnail:category.content.thumbnail.filename,
          }
        })
      }
    })
  },
}
</script>

<style scoped>

</style>
