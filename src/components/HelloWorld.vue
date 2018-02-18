<template>
  <div class="hello">
    <User username='sh7dm'></User>
    <h1>VS</h1>
    <User username='torvalds'></User>
  </div>
</template>

<script>
import User from './User'

export default {
  components: { User },
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.hello {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
</style>
