<template>
  <div class="search-area">
    <input v-model="searchedUser" placeholder="Enter name or ID..." />
  </div>

  <!-- Searched -->
  <div class="user-info" v-if="!showAllUsers">
    <div class="user" v-for="(user, index) in filteredUsers" :key="index">
      <div class="first-sec">
        <p>
          Name: <span>{{ user.name }}</span>
        </p>
        <p>
          ID: <span>{{ user._id }}</span>
        </p>
        <p>
          Gender: <span>{{ user.gender }}</span>
        </p>
      </div>
      <div class="second-sec">
        <p>
          Email: <span>{{ user.email }}</span>
        </p>
        <p>
          Address: <span>{{ user.address }}</span>
        </p>
      </div>
      <div class="third-sec">
        <p>
          Register Time: <span>{{ user.registered }}</span>
        </p>
      </div>
      <div class="fourth-sec">
        <p>
          About: <span>{{ user.about }}</span>
        </p>
      </div>
    </div>
  </div>

  <!-- All Users -->
  <div class="user-info" v-if="showAllUsers">
    <div class="user" v-for="(user, index) in users" :key="index">
      <div class="first-sec">
        <p>
          Name: <span>{{ user.name }}</span>
        </p>
        <p>
          ID: <span>{{ user._id }}</span>
        </p>
        <p>
          Gender: <span>{{ user.gender }}</span>
        </p>
      </div>
      <div class="second-sec">
        <p>
          Email: <span>{{ user.email }}</span>
        </p>
        <p>
          Address: <span>{{ user.address }}</span>
        </p>
      </div>
      <div class="third-sec">
        <p>
          Register Time: <span>{{ user.registered }}</span>
        </p>
      </div>
      <div class="fourth-sec">
        <p>
          About: <span>{{ user.about }}</span>
        </p>
      </div>
    </div>
  </div>
  <span class="interviewee">面試者：黃暐倫</span>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      users: [],
      searchedUser: "",
      showAllUsers: true,
    };
  },
  mounted() {
    this.fetchUserData();
  },
  methods: {
    async fetchUserData() {
      try {
        const response = await fetch(
          "https://run.mocky.io/v3/ca6344d4-bf83-4daa-af2f-2e4999b89296"
        );
        const data = await response.json();
        this.users = data;
        console.log(this.users);
      } catch (error) {
        console.error("Failed to fetch user data:", error);
      }
    },
  },
  computed: {
    filteredUsers() {
      return this.users.filter((user) => {
        const searchString = this.searchedUser;
        return (
          user.name.includes(searchString) || user._id.includes(searchString)
        );
      });
    },
  },
  watch: {
    searchedUser(newValue) {
      if (newValue.trim() !== "") {
        this.showAllUsers = false;
      } else {
        this.showAllUsers = true;
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #212529;
  margin-top: 60px;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
}

body {
  background: #eaeaea;
}

.interviewee {
  position: fixed;
  bottom: 0;
  right: 0;
  line-height: 1em;
  padding: 0.5em 0.8em;
  background: white;
  opacity: 0.8;
  border-radius: 1em 0 0 0;
}

.search-area {
  padding: 2rem;
}

.search-area input {
  height: 3rem;
  font-size: 1.8rem;
  padding: 0.2rem;
  border: none;
  border-radius: 5px;
}

.user-info {
  max-width: 180rem;
  margin: 5rem auto;
}

.user {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  max-width: 160rem;
  margin: 2rem auto;
  padding: 1rem;
  font-size: 3rem;
  border: 3px solid black;
  border-radius: 5px;
  text-align: left;
}

.user div p {
  font-weight: 800;
}

.user div p span {
  font-weight: 300;
}

.first-sec,
.second-sec {
  display: flex;
  gap: 20rem;
}

/* 1152px */
@media (max-width: 72em) {
  .user {
    font-size: 2rem;
  }

  .first-sec,
  .second-sec {
    display: block;
  }
}
</style>
