<template>
  <div class="h-14 w-full border-b-1 pl-3 pr-5 flex justify-between bg-white border-trueGray-300">
    <div class="flex items-center">
      <div class="navbar-links" >
        <md-icon @click="openSearch()">search</md-icon>
        <!-- <md-field>
          <md-input v-model="search"></md-input>
        </md-field> -->
      </div>
    </div>
    <div class="flex justify-end items-center">
      <NuxtLink to="/" class="navbar-links">
        <md-icon>notifications</md-icon>
      </NuxtLink>
      <div class="navbar-links">
        <div class="flex justify-between items-center">
          <div>
            <img class="rounded-full w-8 h-8" src="~assets/img/profile.jpg" alt="profile">
          </div>
          <div class="ml-1">Hakan Sarıaslan</div>
          <div class="mt-05 -ml-1">
            <md-icon>expand_more</md-icon>
          </div>
        </div>
      </div>
      <NuxtLink to="/" class="navbar-links ml-0">
        <md-icon>settings</md-icon>
        <div class="navbar-link-descriptions">
          <div class="absolute w-0 h-0 border-l-6 border-r-6 border-b-6 border-sideBar-900 opacity-75" style="border-left-color:transparent; border-right-color:transparent;margin-left: 6px"></div>
          <div class="bg-sideBar-900 opacity-75 text-white px-4 pb-2 pt-1 rounded-full" style="margin-top: 6px; margin-left: -50px;">Settings</div>
        </div>
      </NuxtLink>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        search: 'Search...'
      }
    },
    methods: {
      openSearch() {

      }
    }
  }
</script>

<style scoped>
  md-icon {transition: background-color .15s !important;}
</style>
