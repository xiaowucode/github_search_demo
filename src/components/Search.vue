<template>
  <section class="jumbotron">
    <h3 class="jumbotron-heading">Search Guthub Users</h3>
    <div>
      <input type="text" placeholder="enter the name you search" v-model="keyWord"/>&nbsp;
      <button @click="searchUsers">Search</button>
    </div>
  </section>
</template>

<script>
import axios from 'axios';
export default {
  name: 'Search',
  data() {
    return {
      keyWord: ''
    }
  },
  props: {
    
  },
  methods: {
    searchUsers() {
      this.$bus.$emit('getInfo',{isFirst: false,isLoading: true,error: '',users: []})
      axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
        response => {
          console.log('请求成功了')
          this.$bus.$emit('getInfo',{isLoading: false,error: '',users: response.data.items})
        },
        error => {
          console.log('请求失败了',error.message)
          this.$bus.$emit('getInfo',{isLoading: false,error: error.message,users: []})
        }
      )
    }
  }
}
</script>

<style scoped>

</style>
