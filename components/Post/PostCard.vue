<template>
  <div class="col-lg-6 col-md-6 col-sm-6">
    <NuxtLink :to="post.slug">
      <div class="blog__item post-card">
        <div class="blog__item__pic">
          <img :src="post.thumbnail" :alt="post.slug" />
        </div>
        <div class="blog__item__text">
          <ul>
            <li><i class="fa fa-calendar-o"></i> {{$moment(post.createdAt).format('ll') }}</li>
            <li><i class="fa fa-comment-o"></i> {{post.comment}}</li>
          </ul>
          <h5><NuxtLink :to="post.slug"><a>{{post.title}}</a></NuxtLink></h5>
          <p>{{ post.summary.substring(0,83)+"..." }}</p>
          <NuxtLink :to="post.slug"><a class="blog__btn">READ MORE <span class="arrow_right"></span></a></NuxtLink>
        </div>
      </div>
    </NuxtLink>
  </div>
</template>

<script>
export default {
  name: "PostCard",
  props: ['post'],

}
</script>

<style scoped>

</style>
