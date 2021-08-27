<template>
  <div class="float-left mr-3 min-w-15 relative" v-on:mouseover="toggleSideBar('mouseover')" v-on:mouseleave="toggleSideBar('mouseleave')">
    <div ref="sideBar" class="w-74 min-h-screen bg-sideBar-700 text-sideBar-200 relative">
      <div ref="sideBarHead" class="w-full h-14 bg-sideBar-900 flex items-center justify-between pl-3 text-sideBar-100 text-lg font-semibold">
        <div ref="logo" class="hover:text-red-500 transition duration-150">
          <NuxtLink to="/" style="text-decoration:none;">Laravel Nuxt Admin</NuxtLink>
        </div>
        <div ref="toggleButton" class="absolute" style="right:16px;">
          <md-icon class="cursor-pointer hover:bg-sideBar-400 rounded-md p-4" style="transition: background-color .15s cubic-bezier(.4,0,.2,1);" v-on:click.native="toggleSideBar('click')">menu</md-icon>
        </div>
      </div>
      <div class="w-full pl-2 pr-3 mt-3 transition">
        <NuxtLink to="/" class="menu-links menu-active" style="text-decoration:none;">
          <div>
            <md-icon class="text-xl">dashboard</md-icon>
          </div>
          <div class="menu">Dashboard</div>
        </NuxtLink>
        <NuxtLink to="/" class="menu-links" style="text-decoration:none;">
          <div>
            <md-icon class="text-xl">person</md-icon>
          </div>
          <div class="menu">Users</div>
        </NuxtLink>
        <NuxtLink to="/" class="menu-links" style="text-decoration:none;">
          <div>
            <md-icon class="text-xl">badge</md-icon>
          </div>
          <div class="menu">Clients</div>
        </NuxtLink>
        <NuxtLink to="/" class="menu-links" style="text-decoration:none;">
          <div>
            <md-icon class="text-xl">description</md-icon>
          </div>
          <div class="menu">Projects</div>
        </NuxtLink>
        <NuxtLink to="/" class="menu-links" style="text-decoration:none;">
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
        collapsing: false,
        collapsed: false,
        duration: 300
      }
    },
    methods: {
      toggleSideBar(event) {
        console.log('collapsing: ' + this.collapsing)
        console.log('collapsed: ' + this.collapsed)
        if(event === 'click' || (event === 'mouseleave' && this.collapsed === true)) {
          this.collapsing = true
        } else if(event === 'mouseover') {
          this.sleep(300)
          this.collapsing = false
        }
        if(event === 'mouseleave') {
          this.sleep(300)
        }

        if(this.collapsing === true && this.collapsed === false && event === 'click') {
          this.closeSideBar()
        } else if(this.collapsing === true && this.collapsed === true && event === 'click') {
          this.openSideBar()
        }
        // else if(this.collapsing === false && this.collapsed === true && event === 'mouseover') {
        //   this.openSideBar('mouseover')
        // } else if(this.collapsing === true && this.collapsed === true && event === 'mouseleave') {
        //   this.closeSideBar('mouseleave')
        // }
      },
      openSideBar(event = 'click') {
        let menus = document.querySelectorAll(".menu")
        if (event === 'mouseover') {
          this.classes(this.$refs.sideBar).remove('relative').add('absolute')
        } else {
          this.classes(this.$refs.sideBar).remove('absolute').add('relative')
        }

        // sideBar opening - expand width with transition in duration ms
        this.classes(this.$refs.sideBar).remove('w-15').add('w-74')

        setTimeout(() => {
          // change the display of logo and menu to block
          this.classes(this.$refs.logo).add('block').remove('hidden')

          menus.forEach((menu) => {
            this.classes(menu).add('block').remove('hidden')
          })

          setTimeout(() => {
            this.classes(this.$refs.logo).remove('opacity-0').add('opacity-100')

            menus.forEach((menu) => {
              this.classes(menu).remove('opacity-0').add('opacity-100')
            })

            if(event === 'click') {
              this.collapsed = false;
            } else if(event === 'mouseover') {
              this.collapsed = true;
            }

          }, this.duration / 2)
        }, this.duration / 2)
      },
      closeSideBar(event = 'click') {
        this.classes(this.$refs.sideBar).remove('absolute').add('relative')
        let menus = document.querySelectorAll(".menu")
        // change the display of logo and menu to none
        this.classes(this.$refs.logo).remove('block').add('hidden').add('opacity-0').remove('opacity-100')
        menus.forEach((menu) => {
          this.classes(menu).remove('block').add('hidden').add('opacity-0').remove('opacity-100')
        })

        // sideBar closing - change width with transition
        this.$refs.sideBar.style = "transition: width " + this.duration + "ms"
        this.classes(this.$refs.sideBar).remove('w-74').add('w-15')

        setTimeout(() => {
          this.collapsed = true;
        }, this.duration)
      },
      classes(elem) {
        var list = elem.classList;
        return {
          add:    function(c) { list.add   (c); return this; },
          remove: function(c) { list.remove(c); return this; }
        }
        //     console.log('1')
        // for (var i = 0; i < arguments.length; i++) {
        //   var list = arguments[i].classList;
        //   if(i + 1 < arguments.length) {
        //     await this.classes(arguments[i + 1])
        //     console.log('2')
        //   }
        // }
        // return {
        //     add:    function(c) { list.add   (c); return this; },
        //     remove: function(c) { list.remove(c); return this; }
        // }
      },
      sleepPromise(ms){
        return new Promise(resolve => setTimeout(resolve, ms));
      },
      sleep: async function(ms) {
        await this.sleepPromise(ms);
      }
    }
  }
</script>
