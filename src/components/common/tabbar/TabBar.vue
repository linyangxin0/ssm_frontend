<template>
  <div class="tab-bar-content">
    <div v-for="(item,index) in titles" @click="titleClick(index)">
      <tab-bar-item :title="item"
                    :small-titles="smallTitle[index]"
                    :is-active="currentIndex===index"
                    :path-str="pathStr[index]"
                    @itemClick="itemClick"
                    class="tab-bar-item"
                    ref="child"></tab-bar-item>
    </div>
  </div>
</template>

<script>
  import TabBarItem from "./TabBarItem";
  export default {
    name: "TabBar",
    components: {TabBarItem},
    data(){
      return{
        currentIndex:-1
      }
    },
    props:{
      titles:{
        type:Array,
        default(){
          return [];
        }
      },
      smallTitle:{
        default(){
          return [];
        }
      },
      pathStr:{
        default(){
          return [];
        }
      }
    },
    methods:{
      titleClick(index){
        this.currentIndex=index;
      },
      itemClick(){
        for (let i=0;i<this.$refs.child.length;i++){
          this.$refs.child[i].currentIndex2Init();
        }
      }
    },
    computed:{

    }
  }
</script>

<style scoped>
  .tab-bar-content{
    margin: 10px;
    padding: 20px;
  }


</style>
