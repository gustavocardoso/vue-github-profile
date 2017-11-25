<template>
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

      <ul class="actions">
        <li><button class="btn">List repos</button></li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'userProfile',

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
    margin-left: 0;
    padding: .3em .6em;
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
    }

    .avatar {
      width: 20%;
    }

    .info {
      text-align: left;
      padding: 0 2em;
    }
  }
</style>
