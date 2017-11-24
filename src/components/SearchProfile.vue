<template>
  <div>
    <div class="search-box">
      <input type="text" v-model="profile" placeholder="type a github profile" v-on:focus="clearField" class="profile">
      <button v-on:click="fetchProfile" class="search">search</button>
    </div>

    <div class="loader" v-if="show.loader">
      <div class="bullet"></div>
      <div class="bullet"></div>
      <div class="bullet"></div>
    </div>

    <div v-if="show.user" class="user-profile">
      <img v-bind:src="user.avatar_url" class="avatar">

      <div class="info">
        <h2 class="name">{{ user.name }}</h2>
        <p class="login">{{ user.login }}</p>

        <ul class="meta">
          <li class="repos">Repos: <strong>{{ user.public_repos }}</strong></li>
          <li class="followers">Followers: <strong>{{ user.followers }}</strong></li>
          <li class="following">Following: <strong>{{ user.following }}</strong></li>
        </ul>
      </div>
    </div>

    <p class="error-message" v-if="show.error">{{ error }}</p>
  </div>
</template>

<script>
  export default {
    name: 'SearchProfile',

    data () {
      return {
        apiUrl: 'https://api.github.com/users',
        error: null,
        profile: '',
        show: {
          error: false,
          loader: false,
          user: false
        },
        user: {
          avatar_url: null,
          followers: null,
          following: null,
          location: null,
          login: null,
          name: null,
          public_repos: null
        }
      }
    },

    methods: {
      clearField () {
        this.profile = ''
      },

      fetchProfile () {
        if (!this.user.login || this.user.login !== this.profile) {
          this.error = null
          this.show.error = false
          this.show.user = false
          this.show.loader = true

          setTimeout(() => {
            fetch(`${this.apiUrl}/${this.profile}`)
            .then(response => {
              if (response.ok) {
                return response.json()
              } else {
                throw new Error('User not found')
              }
            })
            .then(data => {
              this.user.avatar_url = data.avatar_url
              this.user.followers = data.followers
              this.user.following = data.following
              this.user.location = data.location
              this.user.login = data.login
              this.user.name = data.name
              this.user.public_repos = data.public_repos
              this.show.loader = false
              this.show.user = true
            })
            .catch(err => {
              this.error = err.message
              this.show.user = false
              this.show.loader = false
              this.show.error = true
            })
          }, 2000)
        }
      }
    }
  }
</script>

<style scoped>
  p {
    margin: 0;
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .profile {
    display: block;
    width: 50%;
    font-size: 1em;
    font-weight: 700;
    text-align: center;
    border-radius: .4em;
    border: 1px solid #ddd;
    margin-bottom: 1em;
    padding: .4em;
    color: #35495E;
  }

  .search {
    display: block;
    font-size: 1em;
    font-weight: 700;
    color: #eee;
    background: #41B883;
    border-radius: .4em;
    border: 0;
    padding: .6em;
  }

  .user-profile {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin: 3em 0;
  }

  .avatar {
    width: 40%;
    border-radius: 2em;
    border: 5px solid #eee;
    box-shadow: 0 .2em 1em 0 rgba(0, 0, 0, 0.2);
    margin-bottom: 1em;
  }

  .name {
    font-size: 2em;
    font-weight: 700;
    letter-spacing: -.05em;
    color: #35495E;
    margin: 0;
  }

  .login {
    font-size: 1.4em;
    color: #41B883;
  }

  .loader {
    display: flex;
    width: 50%;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin: 3em auto 0 auto;
  }

  .bullet {
    width: 1em;
    height: 1em;
    background: #ccc;
    border-radius: 50%;
    margin: 0 1em;
  }

  .bullet:nth-child(1) {
    animation: bounce .5s infinite ease-in-out;
  }
  .bullet:nth-child(2) {
    animation: bounce .5s .1s infinite ease-in-out;
  }
  .bullet:nth-child(3) {
    animation: bounce .5s .2s infinite ease-in-out;
  }

  @keyframes bounce {
    0% {
      transform: scale3d(1, 1, 1);
      opacity: 1;
    }
    50% {
      transform: scale3d(1.4, 1.4, 1.4);
      opacity: .1;
    }
    100% {
      transform: scale3d(1, 1, 1);
      opacity: 1;
    }
  }

  @media screen and (min-width: 50em) {
    .profile {
      width: 22%;
      padding: .6em;
    }

    .user-profile {
      flex-direction: row;
      justify-content: center;
      align-items: center;
      margin: 3em 0;
    }

    .avatar {
      width: 20%;
    }

    .info {
      text-align: left;
      padding: 0 2em;
    }
  }

  .error-message {
    font-size: 1.2em;
    text-transform: uppercase;
    color: #c03;
    margin-top: 2.2em;
  }
</style>
