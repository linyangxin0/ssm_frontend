<template>
  <div class="bar-content">
    <input type="text" class="search-input" v-model="searchText" placeholder="请输入搜索内容">
    <button class="search-btn" @click="searchDevice">搜索</button>
    <button class="all-btn" @click="findAll">全部</button>
    <router-link to="/device/addDevice">
      <button class="btn" v-if="$store.state.isAdmin">新增设备</button>
    </router-link>
  </div>
</template>

<script>
  export default {
    name: "DeviceTopBar",
    data(){
      return{
        searchText:''
      }
    },
    methods:{
      searchDevice(){
        this.$emit("searchDevice",this.searchText)
      },
      findAll(){
        this.$emit("findAll")
        this.searchText=''
      }
    }
  }
</script>

<style scoped>
  .bar-content{
    height: 60px;
  }

  .search-input{
    height: 30px;
    border-radius: 5px;
    border: 1.5px #adadad solid;
    padding-left: 20px;
  }

  .search-btn{
    margin-left: 30px;
    border-radius: 5px;
    height: 35px;
    width: 60px;
    background-color: #c8c8c8;
    border: none;
    cursor: pointer;
  }

  .all-btn{
    margin-left: 30px;
    border-radius: 5px;
    height: 35px;
    width: 60px;
    background-color: #ececec;
    border: 1px #c8c8c8 solid;
    cursor: pointer;
  }

  .btn{
    float: right;
    margin-right: 30px;

    height: 35px;
    width: 100px;
    border-radius: 5px;
    border: 1px #c8c8c8 solid;
    background-color: #fff;
    cursor: pointer;
  }

</style>
