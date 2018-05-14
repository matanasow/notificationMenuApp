<template>
  <div id="app">
    <notificationMenu v-bind:notifications="notifications"  
    v-bind:editedNotificationId="editedNotificationId"
    v-bind:deletedNotificationId="deletedNotificationId">
    </notificationMenu>
  </div>
</template>

<script>
import NotificationMenu from './components/NotificationMenu'

export default {
  name: 'App',
  components:{
     'notificationMenu': NotificationMenu,

  },
  data(){
return {
  notifications: [],
  editedNotificationId: 0,
  deletedNotificationId: 0,
  notificationForPush:
      {
    id: 12,
    type: 'text',
    title: 'Test notification',
    text: 'Test text notification',
    expires: 5
  },
  secondNotificationForPush:
  {
    id: 6,
    type: 'bonus',
    title: 'You win a bonus!',
    requirement: 'Deposit $50 to win',
    expires: 3600
  }
}
},
mounted(){
  setTimeout(() => {
    this.firstNotifications()
    setTimeout(() => {
        this.pushNotification(this.notificationForPush)
        setTimeout(() => {
          this.pushNotification(this.secondNotificationForPush)
        },2000)  
    },2000)
  },2000)
  setTimeout(() => {
    this.editNotification()
    setTimeout(() => {
      this.deleteNotification()
    }, 10000)
  },10000)
},
methods: {
  firstNotifications(){
    this.notifications =[
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
  pushNotification(notification){
    this.notifications.push(notification)
  },
  deleteNotification(){
    let notificationForDeleteId = 4322
    this.deletedNotificationId = notificationForDeleteId
var foundNotificationForDeleteIndex = this.notifications.findIndex(x => x.id == notificationForDeleteId);
    this.notifications.splice(foundNotificationForDeleteIndex,1)
  },
  editNotification(){
    let notificationForEditId = 1321
    this.editedNotificationId = notificationForEditId
      var editedNotification = {    
          id: notificationForEditId,
    type: 'text',
    title: 'Modified test notification',
    text: 'Modified test text notification',
    expires: 360
}
var foundNotificationForEditIndex = this.notifications.findIndex(x => x.id == editedNotification.id);
this.$set(this.notifications, foundNotificationForEditIndex, editedNotification)
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
body {
  background-image: url('https://www.tutorialspoint.com/opencv/images/gaussian_blur.jpg');
  background-repeat: no-repeat;
  background-size: 100%;
}
</style>
