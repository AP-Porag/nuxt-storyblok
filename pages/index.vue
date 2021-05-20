<template>
  <div class="home-page">

    <!-- Blog Section Begin -->
    <section class="blog spad">
      <div class="container">
        <div class="row">
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
                <div class="category_list">
                  <ul>
                    <li><a href="#">All</a></li>
                    <li
                    v-for="category in categories"
                    :key="category.id"
                    ><a href="#">{{category.title}} (20)</a></li>
                  </ul>
                </div>
              </div>
              <div class="blog__sidebar__item">
                <h4>Recent News</h4>
                <div class="blog__sidebar__recent">
                  <div v-if="posts.length > 3">
                    <a href="#" class="blog__sidebar__recent__item"
                    v-for="post in posts"
                       :key="post.id"
                    >
                      <div class="blog__sidebar__recent__item__pic">
                        <img :src="post.thumbnail" alt="">
                      </div>
                      <div class="blog__sidebar__recent__item__text">
                        <h6>{{post.title}}</h6>
                        <span>{{$moment(post.createdAt).format('ll')}}</span>
                      </div>
                    </a>
                  </div>
                  <div v-else>
                    <a href="#" class="blog__sidebar__recent__item"
                       v-for="post in posts"
                       :key="post.id"
                    >
                      <div class="blog__sidebar__recent__item__pic">
                        <img :src="post.thumbnail" alt="" width="40%">
                      </div>
                      <div class="blog__sidebar__recent__item__text">
                        <h6>{{post.title}}</h6>
                        <span>{{$moment(post.createdAt).format('ll')}}</span>
                      </div>
                    </a>
                  </div>
                </div>
              </div>
              <div class="blog__sidebar__item">
                <h4>Search By</h4>
                <div class="blog__sidebar__item__tags">
                  <a href="#"
                     class="text-capitalize"
                  v-for="(tag,index) in tags"
                     :key="index"
                  >{{ tag.title }}
                  <span class="text-capitalize"> ({{tag.taggings_count}})</span>
                  </a>
                </div>
              </div>
            </div>
          </div>
          <div class="col-lg-8 col-md-7">
            <div class="row">
              <PostCard
              v-for="post in posts"
              :key="post.id"
              :post="post"
              />
              <div class="col-lg-12">
                <div class="product__pagination blog__pagination">
                  <a href="#">1</a>
                  <a href="#">2</a>
                  <a href="#">3</a>
                  <a href="#"><i class="fa fa-long-arrow-right"></i></a>
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
import PostCard from "~/components/Post/PostCard";
export default {
  components: {PostCard},
  // asyncData(ctx) {
  //   return ctx.app.$storyapi.get('cdn/stories',{
  //     version:'draft',
  //     starts_with:'blog/'
  //   }).then(res => {
  //     console.log(res)
  //     return {
  //       posts : res.data.stories.map(post => {
  //         return{
  //           id:post.id,
  //           slug:post.slug,
  //           title:post.content.title,
  //           summary:post.content.summary,
  //           content:post.content.content,
  //           thumbnail:post.content.thumbnail.filename,
  //           createdAt:post.created_at,
  //         }
  //       })
  //     }
  //   })
  // },
  asyncData (context) {
    // const options = {
    //   version: 'draft',
    //   starts_with:'/blog'
    // }
    const requests = [
      context.app.$storyapi.get('cdn/stories', {
        version: 'draft',
        starts_with:'blog/'
      }),
      context.app.$storyapi.get('cdn/stories', {
        version: 'draft',
        starts_with:'category/'
      }),
      context.app.$storyapi.get('cdn/tags', {
        version: 'draft',
      }),
      //context.app.$storyapi.get('cdn/stories', options)
    ]

    //use the Promise.all function (recommended)
    return Promise
      .all(requests)
      .then(res => {
        const blog = res[0]
        const category = res[1]
        const tag = res[2]
        console.log(tag)
        //const linksRes = responses[2]

        return {
          posts : blog.data.stories.map(post => {
                    return{
                      id:post.id,
                      slug:post.slug,
                      title:post.content.title,
                      summary:post.content.summary,
                      content:post.content.content,
                      thumbnail:post.content.thumbnail.filename,
                      createdAt:post.created_at,
                    }
                  }),
          categories : category.data.stories.map(category => {
            return{
              id:category.id,
              slug:category.slug,
              title:category.content.title,
              thumbnail:category.content.thumbnail.filename,
            }
          }),
          tags : tag.data.tags.map(tag => {
            return{
              title:tag.name,
              taggings_count:tag.taggings_count,
            }
          }),
        }
      })
      .catch(errors => {
        console.error(errors)
      })
  }


}
</script>

<style>
</style>
