<template>
  <div id="app" :class="pageCss">
    <Navbar @click.native="handleNav($event)" />
    <div id="content">
      <Nuxt />
    </div>
    <Footer />
  </div>
</template>

<script>
import Navbar from "@/components/layout/Navbar";
import Footer from "@/components/layout/Footer";
export default {
  name: "default",
  components: {Footer, Navbar},
  data () {
    return {
      pageCss: 'gradient'
    }
  },
  methods: {
    handleNav: function (event) {
      console.log($nuxt.$route.name)
      this.pageCss = $nuxt.$route.name
    },

  }
}
</script>

<style scoped>
.index {
  background-color: #d4418e;
  background-image: linear-gradient(315deg, #d4418e 0%, #0652c5 74%);
  background-repeat: no-repeat;
}
.corporate {
  background-color: white;
  background-image: none;
  background-repeat: no-repeat;
}
</style>
