<template>
  <div>

    <h2 v-if="firstView">请输入关键字进行搜索</h2>
    <h2 v-else-if="loading">请求中...</h2>
    <h2 v-else-if="errorMsg">{{errorMsg}}</h2>

    <div class="row" v-else>
      <div class="card" v-for="user in users" :key="user.name">
        <a :href="user.url" target="_blank">
          <img :src="user.avatar_url" style='width: 100px'/>
        </a>
        <p class="card-text">{{user.name}}</p>
      </div>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import axios from 'axios'
  export default {

    data () {
      return {
        firstView:true,
        loading:false,
        errorMsg:"",
        users:[]

      }
    },

    mounted () {
      // 绑定自定义事件监听: search
     this.$eventBus.$on("searcch",async (searchName)=>{
       this.firstView = false
       this.loading = true
       const url = `https://api.github.com/search/users?q=${searchName}`
       const response=await axios(url)
       const users=response.data.items.map((item)=>({
          name: item.login,
            url: item.html_url,
            avatar_url: item.avatar_url
       }))
        this.loading = false
        this.users = users
       

     })
    }
  }
</script>

<style scoped>
  .card {
    float: left;
    width: 33.333%;
    padding: .75rem;
    margin-bottom: 2rem;
    border: 1px solid #efefef;
    text-align: center;
  }

  .card > img {
    margin-bottom: .75rem;
    border-radius: 100px;
  }

  .card-text {
    font-size: 85%;
  }

</style>
