<template lang="pug">
  #app
    .contact-list
      .no-friends(v-if="users.length < 1") 
        h1 No friends 😢
        h2 Use to Menu to fetch some new ones
      .box(v-for="user in users")
        .profile-pic
          img(alt="profile-pic"
              :src="user.picture.large")
        .text
          h3 {{ getFullNameForUser(user) }}
          .status
          button(@click="removeUser(user)") REMOVE
    hamburger-menu(:menuIsOpen="menuIsOpen" 
                   @toggle-menu="menuIsOpen = !menuIsOpen")
    transition(name="fade")
      .menu(v-if="menuIsOpen === true")
        ul
          li item 1
          li item 2
          li item 3
          li item 4
        button(@click="fetchRandomUsers") Get New Friends
</template>
<script>
import HamburgerMenu from "../src/components/Navigation/HamburgerMenu.vue";

export default {
  name: "App",
  components: { HamburgerMenu },
  beforeMount() {
    this.fetchRandomUsers();
  },
  data() {
    return {
      menuIsOpen: false,
      numOfUsersToFetch: 10,
      users: []
    };
  },
  methods: {
    fetchRandomUsers: function() {
      fetch(`https://randomuser.me/api/?results=${this.numOfUsersToFetch}`)
        .then(response => response.json())
        .then(data => {
          console.log(data.results);
          this.users = data.results;
        });
    },
    getFullNameForUser: function(user) {
      return `${user.name.first} ${user.name.last}`;
    },
    removeUser: function(user) {
      console.log("Removing..", this.getFullNameForUser(user));
      this.users = this.users.filter(function(usr) {
        return usr != user;
      });
    }
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Lato:wght@400;700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Lato", sans-serif;
  height: 100vh;
  margin: 0;
  overflow: hidden;
  width: 100vw;

  // gradient background
  background: #fc00ff; /* fallback for old browsers */
  background: -webkit-linear-gradient(
    to right,
    #00dbde,
    #fc00ff
  ); /* Chrome 10-25, Safari 5.1-6 */
  background: linear-gradient(
    to right,
    #00dbde,
    #fc00ff
  ); /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
}

// ** Scroll bar **
/* width */
::-webkit-scrollbar {
  width: 8px;
}

/* Track */
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px rgba(255, 255, 255, 0.6);
  border-radius: 10px;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.8);
  border-radius: 10px;
  &:hover {
    background: rgba(255, 255, 255, 1);
  }
}
// **

#app {
  align-items: center;
  display: flex;
  height: 100%;
  justify-content: center;
  overflow: inherit;
  width: 100%;
}

.contact-list {
  align-items: center;
  border-radius: 10px;
  color: white;
  display: flex;
  flex-direction: column;
  height: 80%;
  overflow-x: hidden;
  width: 80%;

  // glass bg
  background: rgba(255, 255, 255, 0.15);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
}

.box {
  // glass bg
  background: rgba(255, 255, 255, 0.1);
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);

  border-radius: 10px;
  color: white;
  display: flex;
  margin: 1rem;
  padding: 1rem;
  width: 500px;

  .profile-pic {
    background-color: red;
    border-radius: 50vh;
    height: 100px;
    overflow: hidden;
    width: 100px;

    img {
      height: 100%;
      width: 100%;
    }
  }
  .text {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    margin: 0 1rem;
    padding: 0 1rem;

    h3 {
      margin-bottom: 1rem;
    }
  }
}

.menu {
  border-radius: 10px;
  background: white;
  box-shadow: 0 8px 32px 0 rgba(31, 38, 135, 0.37);
  bottom: 1rem;
  min-width: 200px;
  padding: 1rem 2rem;
  position: absolute;
  right: 60px;
  transform-origin: bottom right;
  transition: all 0.3s;
  z-index: 99;
}

.no-friends {
  padding: 2rem;
  text-align: center;

  :first-child {
    margin-bottom: 2rem;
  }
}

// Animations
.fade-enter-active,
.fade-leave-active {
  transition: all 0.3s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
  transform: scale(0);
}

@media only screen and (max-width: 769px) {
  .contact-list {
    border-bottom: 1px solid white;
    border-top: 1px solid white;
    border-radius: 0px;
    width: 100%;
  }
  .box {
    width: 90%;
  }
  ::-webkit-scrollbar {
    display: none;
  }
}
</style>
