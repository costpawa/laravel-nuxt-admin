<template>
  <div class="float-left min-w-15 relative z-10" v-on:mouseover="openSideBar('mouseover')" v-on:mouseleave="closeSideBar('mouseleave')">
    <div ref="sideBar" class="w-74 min-h-screen bg-sideBar-700 text-sideBar-200 relative overflow-x-hidden sidebar">
      <div ref="sideBarHead" class="w-full h-14 bg-sideBar-900 flex items-center justify-between pl-3 text-sideBar-100 text-lg font-semibold">
        <div ref="logo" class="transition duration-150 overflow-x-hidden">
          <NuxtLink to="/" class="logo whitespace-no-wrap" style="text-decoration:none;color: #858598 !important;">Laravel Nuxt Admin</NuxtLink>
        </div>
        <div ref="toggleButton" class="absolute" style="right:16px;">
          <md-icon class="cursor-pointer hover:bg-sideBar-400 rounded-md p-4" style="transition: background-color .15s cubic-bezier(.4,0,.2,1);" v-on:click.native="toggleSideBar()">menu</md-icon>
        </div>
      </div>
      <div class="w-full pl-2 pr-3 mt-3 transition">
        <NuxtLink to="/" exact class="menu-links" style="text-decoration:none;">
          <div>
            <md-icon class="text-xl">dashboard</md-icon>
          </div>
          <div class="menu">Dashboard</div>
        </NuxtLink>
        <NuxtLink to="/users" class="menu-links" style="text-decoration:none;">
          <div>
            <md-icon class="text-xl">people</md-icon>
          </div>
          <div class="menu">Users</div>
        </NuxtLink>
        <NuxtLink to="/clients" class="menu-links" style="text-decoration:none;">
          <div>
            <md-icon class="text-xl">badge</md-icon>
          </div>
          <div class="menu">Clients</div>
        </NuxtLink>
        <NuxtLink to="/projects" class="menu-links" style="text-decoration:none;">
          <div>
            <md-icon class="text-xl">description</md-icon>
          </div>
          <div class="menu">Projects</div>
        </NuxtLink>
        <NuxtLink to="/tasks" class="menu-links" style="text-decoration:none;">
          <div>
            <md-icon class="text-xl">checklist</md-icon>
          </div>
          <div class="menu">Tasks</div>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        collapsed: false,
        duration: 500
      }
    },
    methods: {
      toggleSideBar() {
        if(this.collapsed === false) {
          this.closeSideBar()
        } else if(this.collapsed === true) {
          this.openSideBar()
        }
      },
      openSideBar(event = 'click') {
        if(this.collapsed === true) {
          if (event === 'mouseover') {
            this.sideBarAbsolute()
          } else {
            this.sideBarRelative()
          }

          this.sideBarTransitionDuration()
          this.changeClasses(this.$refs.sideBar, 'w-15', 'w-74')

          this.changeClasses(this.$refs.logo, 'hidden', 'block', 'opacity-0', 'opacity-100')
          this.menus().forEach((menu) => {
            this.changeClasses(menu, 'hidden', 'block', 'opacity-0', 'opacity-100')
          })
        }
        if(event === 'click') {
          this.collapsed = false
        }
      },
      closeSideBar(event = 'click') {
        if(event === 'click' || (event === 'mouseleave' && this.collapsed === true)) {
          this.changeClasses(this.$refs.logo, 'block', 'hidden', 'opacity-100', 'opacity-0')
          this.menus().forEach((menu) => {
            this.changeClasses(menu, 'block', 'hidden', 'opacity-100', 'opacity-0')
          })

          this.sideBarTransitionDuration()
          this.changeClasses(this.$refs.sideBar, 'w-74', 'w-15')

          setTimeout(() => {
            this.sideBarRelative()
            this.collapsed = true;
          }, this.duration)
        }
      },
      changeClasses(elem) {
        for (let i = 1; i <= arguments.length; i++) {
          if(i % 2 == 1) {
            this.changeClass(elem).remove(arguments[i])
          } else {
            this.changeClass(elem).add(arguments[i])
          }
        }
      },
      changeClass(elem) {
        let list = elem.classList;
        return {
          add:    function(c) { list.add   (c); return this; },
          remove: function(c) { list.remove(c); return this; }
        }
      },
      sideBarTransitionDuration() {
        return this.$refs.sideBar.style = "transition: width " + this.duration + "ms"
      },
      sideBarAbsolute() {
        return this.changeClasses(this.$refs.sideBar, 'relative', 'absolute')
      },
      sideBarRelative() {
        return this.changeClasses(this.$refs.sideBar, 'absolute', 'relative')
      },
      menus() {
        return document.querySelectorAll(".menu")
      }
    }
  }
</script>

<style scoped>
  .menu-links, .logo , .sidebar .md-icon {
    color: #858598 !important;
  }
  .logo:hover, .menu-links:hover .md-icon {
    color: #f56565 !important;
  }
  .menu-links:hover, .nuxt-link-active, .nuxt-link-exact-active, .nuxt-link-active .md-icon, .nuxt-link-exact-active .md-icon {
    background-color: #1E1E29 !important;
    color: #f56565 !important;
  }
</style>
