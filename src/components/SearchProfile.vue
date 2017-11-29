<template>
  <div>
    <div class="search-box">
      <input type="text" v-model="profile" placeholder="type a github profile" v-on:focus="clearField" v-on:keyup.enter="fetchProfile" class="profile">
    </div>

    <loader v-if="show.loader"></loader>

    <user-profile v-bind:user="user" v-if="show.user"></user-profile>

    <p class="error-message" v-if="show.error">{{ error }}</p>
  </div>
</template>

<script>
  import Loader from './helpers/Loader'
  import UserProfile from './UserProfile'

  export default {
    name: 'SearchProfile',

    components: {
      Loader,
      UserProfile
    },

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
        user: {}
      }
    },

    methods: {
      clearField () {
        this.profile = ''
      },

      fetchProfile () {
        if (!this.user.login || this.user.login !== this.profile) {
          this.user = {}
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
              this.user = data
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

  @media screen and (min-width: 50em) {
    .search-box {
      flex-direction: row;
      justify-content: center;
      align-items: flex-start;
    }

    .profile {
      width: 35%;
      padding: .6em;
    }
  }
</style>
