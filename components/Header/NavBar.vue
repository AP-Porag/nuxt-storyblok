<template>
  <!-- NavBar Section Begin -->
  <div class="navigation_bar bg-warning">
    <div class="container">
      <div class="row">
        <div class="col-lg-3">
          <div class="header__logo">
            <NuxtLink to="/"><a><img src="~/assets/img/logo.png" alt=""></a></NuxtLink>
          </div>
        </div>
        <div class="col-lg-6">
          <nav class="header__menu">
            <ul class="text-center">
              <li class="active"><NuxtLink to="/"><a>Home</a></NuxtLink></li>
              <li><NuxtLink to="/categories"><a>Categories</a></NuxtLink>
                <ul class="header__menu__dropdown text-left">
                  <li
                  v-for="category in categories"
                  :key="category.id"
                  >
                    <NuxtLink :to="'/'+category.slug"><a>{{category.title}}</a></NuxtLink>
                  </li>
                  <li>
                    <NuxtLink to="/shoping-cart"><a>Shoping Cart</a></NuxtLink>
                  </li>
                  <li>
                    <NuxtLink to="/checkout"><a>Check Out</a></NuxtLink>
                  </li>
                  <li>
                    <NuxtLink to="/blog-details"><a>Blog Details</a></NuxtLink>
                  </li>
                </ul>
              </li>
              <li><NuxtLink to="/about"><a>about</a></NuxtLink></li>
            </ul>
          </nav>
        </div>
      </div>
      <div class="humberger__open">
        <i class="fa fa-bars"></i>
      </div>
    </div>
  </div>
  <!-- NavBar Section End -->
</template>

<script>
import Header from "~/components/Header/Header";
import TopBar from "~/components/Header/TopBar";
export default {
  name: "NavBar",
  components: {TopBar, Header},
  props: ['categories']

}
</script>

<style scoped>

</style>
