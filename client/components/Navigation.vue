<template>
  <div>
    <div>
      <NuxtLink
        to="/"
      >{{ getCurrentRoute() }}</NuxtLink>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return{

      }
    },
    methods: {
      getCurrentRoute() {
        let splitRoute = this.splitRoute()
        // splitRoute.array.forEach(element => {

        // });
        return splitRoute
      },
      splitRoute() {
        let splitTheRoute = $nuxt.$route.path.split("/")
        return splitTheRoute
      },
    }
  }
</script>
