<template>
  <navbar
      :pages="pages"
      :activePages="activePage"
      :nav-link-click="(index:number) => activePage = index"
  >
  </navbar>

  <page-viewer
      :page="pages[activePage]"
  ></page-viewer>
</template>

<script lang="ts">
import PageViewer from './PageViewer.vue'
import Navbar from './Navbar.vue'

export default {
  components: {
      PageViewer,
      Navbar
  },
  data() {
      return {
          activePage: 0,
          currentUser: 0,
          pages: [
              {
                  link: {text: 'Home', url: 'index.html'},
                  pageTitle:'Home Page',
                  content:'This is the home content'
              },
              {
                  link: {text: 'Profile', url: 'profile.html'},
                  pageTitle:'Profile Page',
                  content:'This is the profile content'
              },
              {
                  link: {text: 'Credit', url: 'credit.html'},
                  pageTitle:'Credit Page',
                  content:'This is the credit content'
              }
          ]
      };
  }
}
</script>

<!-- Adding the 'scoped' attribute limits the scope of the defined styles to this component -->
<style scoped>

</style>