<template>
  <div class="notificationMenu">
   <div class="dropdown">
  <button class="dropbtn" @click="toggleDropdown">
    <div v-bind:notificationsLenghtCounter="notificationsLenghtCounter">{{notificationsLenghtCounter}}</div>
    </button> 
  <div class="dropdown-content arrow_box" v-if="showDropdown" v-bind:disable="copyNotifications">
    <a class="border-top-bottom" v-bind:key="notification.id" v-for="notification in copyNotifications" href="#">
      <div>
        <!-- v-bind:class="{fadeOutRight: watchForDeletedNotification || fadeIn: watchForEditedNotification}" -->
<img class="image-size" v-bind:href="notification.link" v-if="notification.image" v-bind:src="notification.image"/>
      <div>
      {{notification.title}}
      </div>
      <div>
      {{notification.text || notification.requirement}}
      </div>
      </div>
    </a>
  </div>
</div>
</div>
</template>

<script>
export default {
  name: 'NotificationMenu',
  props: ['notifications', 'deletedNotificationId', 'editedNotificationId'],
  data () {
    return {
      copyNotifications: [],
      notificationsLenghtCounter: "",
      showDropdown:false,
    }
  },
  watch: {
    notifications(val){
      this.copyNotifications = this.notifications
      this.notificationsLenghtCounter = this.notificationsCount()
    }
    // deletedNotificationId: function(val){
    //   debugger
      
    //   this.deletedNotificationId = this.deletedNotificationId
    // },
    // editedNotificationId: function(val){
    //   debugger
      
    //   this.editedNotificationId = this.editedNotificationId
    // }
  },
  mounted(){
    this.watchForExpiredNotifacations();
  },
  methods: {
    watchForExpiredNotifacations() {
      setInterval(() => {
         let left = this.copyNotifications.filter((notification) => {
            notification.expires--;
            return notification.expires > 0 || notification.type == 'Promotion';
         });

         this.copyNotifications = left;
      },1000)
    },
    notificationsCount() {
      return ("Notifications(" + this.copyNotifications.filter(n => n.type !== 'bonus').length + ")")
    },

    // If notifications should be grouped 

  //   organize(notifications, groupBy) {
  //   return notifications.reduce ( (result, obj) => {
  //       groupBy.reduce( (result, grp, i) => 
  //           result[obj[grp]] || (result[obj[grp]] = i == 0 ? [] : {}), result).push(obj);
  //       return result;
  //   }, {});
  // }

  toggleDropdown () {
    this.showDropdown = !this.showDropdown
},
hideDropdown () {
    this.showDropdown = false
},
watchForDeletedNotification(notification){
  return
  notification.id == this.deletedNotificationId || 
      (notification.expires == 0 && notification.type !== 'Promotion')
      
},
watchForEditedNotification(notification){
  return
      notification.id == this.editedNotificationId
}
  }
}
</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
.item-size {
max-width: 300px;
max-height: 100px;
}
.image-size{
  max-width: 100px;
    height: 50px;
}
.arrow_box {
	position: relative;
	background: #88b7d5;
}
.arrow_box:after, .arrow_box:before {
	bottom: 100%;
	left: 50%;
	border: solid transparent;
	content: " ";
	height: 0;
	width: 0;
	position: absolute;
	pointer-events: none;
}

.arrow_box:after {
	border-color: rgba(136, 183, 213, 0);
	border-bottom-color:whitesmoke;
	border-width: 30px;
	margin-left: -30px;
}
.arrow_box:before {
	border-color: rgba(194, 225, 245, 0);
	border-bottom-color: #c2e1f5;
	margin-left: -36px;
}
.dropbtn {
    background-color: white;
    color: white;
    padding: 16px;
    font-size: 16px;
    border-radius: 15%;
    cursor: pointer;
}
.dropdown {
    position: relative;
    display: inline-block;
}
.dropdown-content {
    display: none;
    position: relative;
    background-color: #f1f1f1;
    min-width: 160px;
    box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
    z-index: 1;
    margin-top: 30px;
    border-radius: 5%;
}
.dropdown-content a {
    color: black;
    padding: 12px 16px;
    text-decoration: none;
    display: block;
}
.dropdown-content a:hover {background-color: #cff1fc;
border-radius: 5%;}
 .dropdown-content {
    display: block;
}
.dropdown:hover .dropbtn {
    background-color: #e7f1f8;
}
.fadeOutRight {
  -webkit-animation-name: fadeOutRight;
  animation-name: fadeOutRight;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
  }
  @-webkit-keyframes fadeOutRight {
  0% {
  opacity: 1;
  }
  100% {
  opacity: 0;
  -webkit-transform: translate3d(100%, 0, 0);
  transform: translate3d(100%, 0, 0);
  }
  }
  @keyframes fadeOutRight {
  0% {
  opacity: 1;
  }
  100% {
  opacity: 0;
  -webkit-transform: translate3d(100%, 0, 0);
  transform: translate3d(100%, 0, 0);
  }
  }
         .fadeIn {
  -webkit-animation-name: fadeIn;
  animation-name: fadeIn;
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
  }
  @-webkit-keyframes fadeIn {
  0% {opacity: 0;}
  100% {opacity: 1;}
  }
  @keyframes fadeIn {
  0% {opacity: 0;}
  100% {opacity: 1;}
  } 
  .border-top-bottom{
    border-color: rgb(221, 218, 218);
    border-top: 3px;
  }
</style>
