<template>
  <div>
    <div v-if='user'>
      <img :src='user.avatar_url' width="200">
      <p>{{ user.name }}</p>
      <p><a :href='user.html_url'>{{ user.login }}</a></p>
      <p>Id: {{ user.id }}</p>
      <p>Public repos count: {{ user.public_repos }}</p>
      <p>Public gists count: {{ user.public_gists }}</p>
      <p>Followers count: {{ user.followers }}</p>
      <p>Stars count: {{ starsTotal }}</p>
    </div>
    <div v-else>
      User not found!
    </div>
  </div>
</template>

<script>
export default {
  name: 'User',
  data () {
    return {
      user: {},
      repos: [],
      starsTotal: 0
    }
  },
  props: [ 'username' ],
  async created () {
    try {
      this.user = (await this.$http.get('users/' + this.username)).data
    } catch (err) {
      this.user = undefined
      console.error('Failed to get user ' + this.username + ':', err)
    }

    try {
      this.repos = (await this.$http.get('users/' + this.username + '/repos')).data
    } catch (err) {
      this.repos = undefined
      console.error('Failed to get repos of the user ' + this.username + ':', err)
    }
  },
  watch: {
    async username () {
      try {
        this.user = (await this.$http.get('users/' + this.username)).data
      } catch (err) {
        this.user = undefined
        console.error('Failed to get user ' + this.username + ':', err)
      }

      try {
        this.repos = (await this.$http.get('users/' + this.username + '/repos')).data
      } catch (err) {
        this.repos = undefined
        console.error('Failed to get repos of the user ' + this.username + ':', err)
      }
    },
    repos () {
      this.repos.forEach(repo => {
        this.starsTotal += repo.stargazers_count
      })
    }
  }
}
</script>

<style scoped>
a {
  color: #777;
  text-decoration: none;
}
</style>
