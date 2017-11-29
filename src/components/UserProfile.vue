<template>
  <div class="user-container">
    <div class="user-profile">
      <img v-bind:src="user.avatar_url" class="avatar">

      <div class="info">
        <h2 class="name">{{ user.name }}</h2>
        <p class="login">{{ user.login }}</p>

        <ul class="meta">
          <li class="repos">Repos: <strong>{{ user.public_repos }}</strong></li>
          <li class="followers">Followers: <strong>{{ user.followers }}</strong></li>
          <li class="following">Following: <strong>{{ user.following }}</strong></li>
        </ul>

        <button class="btn" v-on:click.stop.prevent="loadRepos" v-if="show.button">
          <span v-if="!show.loader">List repos</span>
          <span v-else>Loading</span>
        </button>
      </div>
    </div>

    <list-repos v-bind:reposUrl="reposUrl" v-if="show.repos"></list-repos>
  </div>
</template>

<script>
  import Loader from './helpers/Loader'
  import ListRepos from './ListRepos'

  export default {
    name: 'userProfile',

    components: {
      ListRepos,
      Loader
    },

    data () {
      return {
        reposUrl: this.user.repos_url,
        show: {
          button: true,
          loader: false,
          repos: false
        }
      }
    },

    methods: {
      loadRepos () {
        this.show.loader = true
        this.show.repos = false

        setTimeout(() => {
          this.show.repos = true
          this.show.loader = false
          this.show.button = false
        }, 3000)
      }
    },

    props: {
      user: {
        type: Object,
        required: true,
        default: {}
      }
    }
  }
</script>

<style scoped>
  .user-container {
    display: block;
    width: 100%;
    margin: 0 auto;
  }

  .user-profile {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: #fafafa;
    border-radius: 2em;
    margin: 3em 0;
    padding: 2em;
  }

  .avatar {
    width: 12em;
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
    margin: 0;
  }

  .btn {
    display: block;
    font-size: .8em;
    font-weight: normal;
    text-transform: uppercase;
    text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.2);
    color: #eee;
    background: #666;
    border-radius: .4em;
    border: 0;
    margin: 1.6em auto 0 auto;
    padding:  .6em;
    cursor: pointer;
  }

  .btn:hover {
    text-shadow: none;
    color: #fff;
    background: #41B883;
  }

  @media screen and (min-width: 50em) {
    .user-profile {
      flex-direction: row;
      justify-content: center;
      align-items: center;
      margin: 3em 0;
      padding: 3em 0 2em 0;
    }

    .btn {
      margin: 1.6em 0 0 0;
    }

    .avatar {
      width: 15em;
    }

    .info {
      text-align: left;
      padding: 0 2em;
    }
  }
</style>
