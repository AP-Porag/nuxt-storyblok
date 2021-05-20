<template>
  <div class="home-page">

    <!-- Blog Section Begin -->
    <section class="blog spad">
      <div class="container">
        <div class="row">
          <div class="col-lg-8 col-md-7">
            <div class="single_post">
              <div class="post_topper">
                <h3>{{title}}</h3>
              </div>
              <div class="post_thumbnail">
                <img :src="thumbnail" :alt="slug" />
              </div>
              <div class="post_body">
                <div v-html="$md.render(content)" class="mt-8"></div>
                <p
                ></p>
              </div>
              <div class="post_tags">
                <h3>
                  <b-badge
                    variant="warning"
                    class="text-white mr-2"
                    v-for="(tag,index) in tags"
                    :key="index"
                  >{{ tag }}</b-badge>
                </h3>
              </div>
              <div class="post_comment"></div>
            </div>
          </div>
          <div class="col-lg-4 col-md-5">
            <div class="blog__sidebar">
              <div class="blog__sidebar__search">
                <form action="#">
                  <input type="text" placeholder="Search...">
                  <button type="submit"><span class="icon_search"></span></button>
                </form>
              </div>
              <div class="blog__sidebar__item">
                <h4>Categories</h4>
                <ul>
                  <li><a href="#">All</a></li>
                  <li><a href="#">Beauty (20)</a></li>
                  <li><a href="#">Food (5)</a></li>
                  <li><a href="#">Life Style (9)</a></li>
                  <li><a href="#">Travel (10)</a></li>
                </ul>
              </div>
              <div class="blog__sidebar__item">
                <h4>Recent News</h4>
                <div class="blog__sidebar__recent">
                  <a href="#" class="blog__sidebar__recent__item">
                    <div class="blog__sidebar__recent__item__pic">
                      <img src="~/assets/img/blog/sidebar/sr-1.jpg" alt="">
                    </div>
                    <div class="blog__sidebar__recent__item__text">
                      <h6>09 Kinds Of Vegetables<br /> Protect The Liver</h6>
                      <span>MAR 05, 2019</span>
                    </div>
                  </a>
                  <a href="#" class="blog__sidebar__recent__item">
                    <div class="blog__sidebar__recent__item__pic">
                      <img src="~/assets/img/blog/sidebar/sr-2.jpg" alt="">
                    </div>
                    <div class="blog__sidebar__recent__item__text">
                      <h6>Tips You To Balance<br /> Nutrition Meal Day</h6>
                      <span>MAR 05, 2019</span>
                    </div>
                  </a>
                  <a href="#" class="blog__sidebar__recent__item">
                    <div class="blog__sidebar__recent__item__pic">
                      <img src="~/assets/img/blog/sidebar/sr-3.jpg" alt="">
                    </div>
                    <div class="blog__sidebar__recent__item__text">
                      <h6>4 Principles Help You Lose <br />Weight With Vegetables</h6>
                      <span>MAR 05, 2019</span>
                    </div>
                  </a>
                </div>
              </div>
              <div class="blog__sidebar__item">
                <h4>Search By</h4>
                <div class="blog__sidebar__item__tags">
                  <a href="#">Apple</a>
                  <a href="#">Beauty</a>
                  <a href="#">Vegetables</a>
                  <a href="#">Fruit</a>
                  <a href="#">Healthy Food</a>
                  <a href="#">Lifestyle</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- Blog Section End -->

  </div>
</template>

<script>
export default {
  name: "index",
  asyncData(ctx) {
    return ctx.app.$storyapi.get('cdn/stories/blog/'+ctx.params.postId,{
      version:'draft'
    }).then(res => {
      console.log(res)
        return{
          id:res.data.story.content.id,
          category:res.data.story.content.id,
          tags:res.data.story.tag_list,
          title:res.data.story.content.title,
          slug:res.data.story.slug,
          summary:res.data.story.content.summary,
          content:res.data.story.content.content,
          thumbnail:res.data.story.content.thumbnail.filename,
          createdAt:res.data.story.created_at,
          comment:res.data.story.content.id
        }
    })
  }
}
</script>

<style scoped>

</style>
