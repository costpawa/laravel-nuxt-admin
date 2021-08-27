<template>
  <div class="float-left mr-3">
    <div ref="sideBar" class="w-74 min-h-screen bg-sideBar-700 text-sideBar-200 relative">
      <div ref="sideBarHead" class="w-full h-14 bg-sideBar-900 flex items-center justify-between pl-3 text-sideBar-100 text-lg font-semibold">
        <div ref="logo" class="hover:text-red-500 transition">
          <NuxtLink to="/" style="text-decoration:none;">Laravel Nuxt Admin</NuxtLink>
        </div>
        <div ref="toggleButton" class="absolute" style="right:16px;">
          <md-icon class="cursor-pointer hover:bg-sideBar-400 rounded-md p-4" style="transition: background-color .15s cubic-bezier(.4,0,.2,1);" v-on:click.native="toggleSideBar()">menu</md-icon>
        </div>
      </div>
      <div class="w-full ml-3 mt-3 transition" ref="menu">asda</div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        visible: true,
        duration: 300
      }
    },
    methods: {
      toggleSideBar() {

        //this.classes(this.$refs.logo, this.$refs.menu).add('zaa')
        if(this.visible === true) {
          // change the display of logo and menu to none
          this.classes(this.$refs.logo).remove('block').add('hidden').add('opacity-0').remove('opacity-100').add('duration-' + this.duration)
          this.classes(this.$refs.menu).remove('block').add('hidden').add('opacity-0').remove('opacity-100').add('duration-' + this.duration)

          // sideBar closing - change width with transition
          this.$refs.sideBar.style = "transition: width " + this.duration + "ms"
          this.classes(this.$refs.sideBar).remove('w-74').add('w-15')

          // declare visibility to false
          this.visible = false;
        } else {
          // sideBar opening - expand width with transition in duration ms
          this.classes(this.$refs.sideBar).remove('w-15').add('w-74')

          setTimeout(() => {
            // change the display of logo and menu to block
            this.classes(this.$refs.logo).add('block').remove('hidden')
            this.classes(this.$refs.menu).add('block').remove('hidden')

            setTimeout(() => {
              this.classes(this.$refs.logo).remove('opacity-0').add('opacity-100')
              this.classes(this.$refs.menu).remove('opacity-0').add('opacity-100')
            }, this.duration / 2)
          }, this.duration / 2)

          // change visibility to true
          this.visible = true;
        }
      },
      classes(elem) {
        var list = elem.classList;
        return {
          add:    function(c) { list.add   (c); return this; },
          remove: function(c) { list.remove(c); return this; }
        }
        // let results = []
        // for (var i = 0; i < arguments.length; i++) {
        //   var list = arguments[i].classList;
        //   results.push({
        //       add:    function(c) { list.add   (c); return this; },
        //       remove: function(c) { list.remove(c); return this; }
        //   })
        // }
        // console.log({...results})
        // return {...results};
      }
    }
  }
</script>
