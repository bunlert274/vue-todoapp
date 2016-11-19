<template>
  <div id="app">

    <section class="hero is-info main-nav">
      <div class="hero-header">
        <div class="container">
          <nav class="nav">
            <div class="nav-left"></div>
            <div class="nav-center">
              <h1 class="nav-item is-brand">Todo Application</h1>
            </div>
            <div class="nav-right"></div>
          </nav>
        </div>
      </div>
    </section>

    <section class="section">
      <div class="container">
        <div class="columns">
          <div class="column is-half is-offset-one-quarter">
            <form v-on:submit.prevent="setLocalStorage()" class="control">
              <div class="control has-addons">
                <input type="text" class="input is-expanded" required v-model="xmessage" placeholder="What do you want to do!">
                <button type="submit" class="button is-primary">
                  Insert!
                </button>
              </div>
            </form>

            <div class="level" v-for="item in items">
              
              <div class="level-left">
                <div class="level-item">
                  <p class="subtitle is-6">{{ item.message }}</p>
                </div>
              </div>

              <div class="level-right">
                <div class="level-item">
                  <button type="button" @click="removeItem(item.idx)" class="button is-small is-info">Complete</button>
                </div>
              </div>
            </div>
            

          </div>
        </div>
      </div>
    </section>

  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [],
      xmessage: ''
    }
  },
  beforeMount() {
    this.getLocalStorage()
  },
  computed: {
  },
  methods: {
    setLocalStorage: function() {
      let message = this.xmessage
      let count = this.getItem() + 1
      window.localStorage.setItem(count ,message)
      this.xmessage = ''
      this.getLocalStorage()
    },
    getLocalStorage: function() {
      if(typeof(Storage) !== 'undefined') {
        this.items = []
        for(var i in window.localStorage) {
          this.items.push({'idx': i, 'message': window.localStorage.getItem(i)})
        }
      }
    },
    getItem: function() {
      return window.localStorage.length
    },
    removeItem: function(idx) {
      // alert(idx);
      if(typeof(Storage) !== 'undefined') {
        window.localStorage.removeItem(idx)
        this.getLocalStorage()      
      }
    }
  }

}
</script>
<style lang="sass">
  @import "~bulma/sass/utilities/_all";
  @import "~bulma/sass/base/_all";
  @import "~bulma/sass/layout/hero";
  @import "~bulma/sass/layout/section";
  @import "~bulma/sass/grid/_all";
  @import "~bulma/sass/elements/button";
  @import "~bulma/sass/elements/form";  
  @import "~bulma/sass/components/level";
  @import "~bulma/sass/components/nav";

  html {
    background-color: $white;
  }

  body {
    color: #4e4e4e;
    padding: 0px !important;
    margin: 0px !important;

    .level {
      padding-bottom: 0.3em;
      border-bottom: 1px solid $grey-lighter;
    }

  }

</style>