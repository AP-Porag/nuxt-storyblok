<template>
  <div>
    <Header/>
    <main class="full-page">
      <Hero/>
      <Nuxt />
    </main>
    <Footer/>
  </div>
</template>

<style>
*{
  box-sizing: border-box;
}
body{
  font-family: 'Dosis', sans-serif;
}
</style>
<script>
import Header from "~/components/Header/Header";
import Footer from "~/components/Footer/Footer";
import Hero from "~/components/Hero/Hero";
export default {
  components: {Hero, Footer, Header}
}
</script>
