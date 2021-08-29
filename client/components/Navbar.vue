<template>
  <div class="h-14 w-full border-b-1 pl-3 pr-5 flex justify-between bg-white border-trueGray-300">
    <div class="flex items-center">
      <div class="navbar-links" >
        <!-- <md-icon @click="openSearch()">search</md-icon>
        <md-field>
          <md-input v-model="search"></md-input>
        </md-field> -->
      </div>
    </div>
    <div class="flex justify-end items-center">
      <NuxtLink to="/" class="navbar-links" title="Notifications">
        <md-icon>notifications</md-icon>
      </NuxtLink>
      <div class="navbar-links" @click="profileToggle = !profileToggle">
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
      <!-- <XyzTransition xyz="fade-100% origin-top short-100% ease-in-out-back">
        <div v-if="profileToggle">
          zaaa
        </div>
      </XyzTransition> -->

      <NuxtLink to="/" class="navbar-links ml-0" title="Settings">
        <md-icon>settings</md-icon>
      </NuxtLink>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        profileToggle: false
      }
    }
  }
</script>

<style scoped>
  .md-icon {transition: color .15s !important;}
  .navbar-links:hover .md-icon {
    color: #1E1E29 !important;
  }
</style>
