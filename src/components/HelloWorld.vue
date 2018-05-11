<template>
  <div class="hello">
      <button v-on:click="isOpened = !isOpened">
      </button>
      {{copyNotifications}}
      <ul v-show="isOpened" role="menu">
      <li v-bind:key="notification.id" v-for="notification in copyNotifications">
        {{notification.type}}
      </li>
    </ul>
    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: ['notifications'],
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      isOpened: false,
      copyNotifications: []
    }
  },
  watch: {
    notifications: function(val){
      this.copyNotifications = this.notifications;
    }
  },
  mounted: function(){
    this.watchForExpiredNotifacations();
  },
  methods: {
    watchForExpiredNotifacations() {
      setInterval(() => {
        console.log(this.copyNotifications)
         let left = this.copyNotifications.filter((notification) => {
            notification.expires--;
            return notification.expires > 0;
         });

         this.copyNotifications = left;
      },10)
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
