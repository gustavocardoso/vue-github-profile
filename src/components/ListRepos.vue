<template>
  <div>
    <h3 class="page-title">Repositories</h3>
    <div class="repos">
      <div class="repo" v-for="(repo, index) in repos" :key="index">
        <h3 class="title">{{ repo.name }}</h3>

        <p class="description">{{ repo.description }}</p>

        <div class="meta">
          <p class="language">Language: <strong>{{ repo.language }}</strong></p>
          <p class="stars">Stars <strong>{{ repo.stargazers_count }}</strong></p>
        </div>

        <a v-bind:href="repo.url" target="_blank" class="link">view this repo</a>
      </div>
    </div>

    <p class="error-message" v-if="showError">{{ error }}</p>
  </div>
</template>

<script>
  export default {
    name: 'listRepos',

    data () {
      return {
        repos: [],
        showError: false,
        showRepos: false
      }
    },

    created () {
      const url = this.reposUrl

      fetch(url)
      .then(response => {
        if (response.ok) {
          return response.json()
        } else {
          throw new Error('Repos not found')
        }
      })
      .then(data => {
        this.repos = data
        this.showRepos = true
      })
      .catch(err => {
        this.error = err.message
        this.showRepos = false
        this.showError = true
      })
    },

    props: {
      reposUrl: {
        type: String,
        required: true,
        default: ''
      }
    }
  }
</script>

<style scoped>
  .page-title {
    font-size: 1.6em;
  }

  .repos {
    display: flex;
    flex-direction: column;
  }

  .repo {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    border-radius: 1em;
    padding: 1em 2em;
    margin-bottom: 2em;
  }

  .repo:nth-child(odd) {
    background: #eee;
  }

  .meta {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin-top: 1em;
  }

  .meta .language {
    margin-right: .7em;
  }

  .meta .stars {
    margin-left: .7em;
  }

  .link {
    display: inline-block;
    font-size: 1em;
    text-shadow: 1px 1px 0 rgba(0, 0, 0, 0.2);
    text-decoration: none;
    color: #eee;
    background: #41B883;
    border-radius: .4em;
    border: 0;
    margin: 1.6em auto 0 auto;
    padding: .3em .6em;
    cursor: pointer;
  }

  .link:hover {
    text-shadow: none;
    color: #fff;
    background: #222;
  }

  @media screen and (min-width: 50em) {
    .repos {
      flex: 1;
      flex-direction: row;
      flex-wrap: wrap;
      justify-content: space-between;
      align-content: flex-start;
    }

    .repo {
      width: 45%;
      background: #eee;
      margin-bottom: 4em;
    }
  }
</style>
