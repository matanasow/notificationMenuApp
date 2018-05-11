<template>
  <div id="app">
    <hello v-bind:notifications="notifications">
    </hello>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components:{
     'Hello': HelloWorld,

  },
  data(){
return {
  notifications: []
}
},
mounted: function(){
  setTimeout(() => {
    this.firstNotifications();
    setTimeout(() => {
        this.secondNotifications();
        setTimeout(() => {
          this.thirdNotifications();
        },2000)  
    },2000)
  },2000)
 
},
methods: {
  firstNotifications: function(){
    console.log("1")
    this.notifications = [

  {
    id: 1321,
    type: 'text',
    title: 'Test notification',
    text: 'Test text notification',
    expires: 3600
  },
  {
    id: 4322,
    type: 'bonus',
    title: 'You win a bonus!',
    requirement: 'Deposit $50 to win',
    expires: 3600
  },
  {
    id: 5453,
    type: 'Promotion',
    image: 'http://www.absolat.com/images/promotion-in-marketing.jpg',
    title: '%30 off on sports betting',
    link: 'https://www.google.com/',
  },
  {
    id: 5236,
    type: 'text',
    title: 'Test notification',
    text: 'Test text notification',
    expires: 5
  }
];
  },
  secondNotifications: function(){
    console.log("2")
    this.notifications = [

  {
    id: 1321,
    type: 'text',
    title: 'Test notification',
    text: 'Test text notification',
    expires: 3600
  },
  {
    id: 4322,
    type: 'bonus',
    title: 'You win a bonus!',
    requirement: 'Deposit $50 to win',
    expires: 3600
  }
];
  },
  thirdNotifications: function(){
    console.log("3")
    this.notifications = [

  {
    id: 1321,
    type: 'text',
    title: 'Test notification',
    text: 'Test text notification',
    expires: 3600
  },
  {
    id: 4322,
    type: 'bonus',
    title: 'You win a bonus!',
    requirement: 'Deposit $50 to win',
    expires: 3600
  },
  {
    id: 5453,
    type: 'Promotion',
    image: 'http://www.absolat.com/images/promotion-in-marketing.jpg',
    title: '%30 off on sports betting',
    link: 'https://www.google.com/',
  },
  {
    id: 5236,
    type: 'text',
    title: 'Test notification',
    text: 'Test text notification',
    expires: 5
  }
];
  }
}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
