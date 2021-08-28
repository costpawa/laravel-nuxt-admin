<template>
  <div>
    <div>
      <div class="text-xl ml-1">{{ pageTitlePlural }}</div>
      <NuxtLink :to="`/${page}/new`" class="-ml-1 my-3 block">
        <md-button class="md-dense md-raised md-primary">Create New {{ pageTitleSingular }}</md-button>
      </NuxtLink>
    </div>
    <!-- <Table
      :page = "page"
      :pageTitle = "pageTitlePlural"
    /> -->
  </div>
</template>

<script>
  export default {
    data() {
      return {
        page: "clients",
        pageTitleSingular: "Client",
        pageTitlePlural: "Clients",
      }
    }
  }
</script>
