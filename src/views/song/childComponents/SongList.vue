<template>
  <div class="list-content">
    <div v-if="songList.length==0" class="none-content">
      <span class="none-text">无可匹配项,请检查是否输入正确关键词.</span>
    </div>
    <table v-if="songList.length!=0">
      <tr>
        <th>序号</th>
        <th>名称</th>
        <th>描述</th>
        <th>歌手</th>
        <th>更新时间</th>
        <th>状态</th>
        <th v-if="$store.state.isAdmin">操作</th>
      </tr>
      <tr v-for="item in songList">
        <td>{{item.id}}</td>
        <td>{{item.name}}</td>
        <td>{{item.info}}</td>
        <td>{{item.author}}</td>
        <td>{{item.updateTime|showDate}}</td>
        <td v-if="item.status!=1">设计中</td>
        <td v-if="item.status==1" class="text-red">发布</td>
        <td v-if="$store.state.isAdmin">
          <button class="list-btn" @click="editSong(item)">编辑</button>
          <button class="list-btn" @click="delSong(item.id)">删除</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>

import {formatDate} from "@/common/utils";

export default {
    name: "SongList",
    filters:{
      showDate:function (value) {
        let date = new Date(value);
        return formatDate(date, 'yyyy-MM-dd')
      }
    },
    props:{
      songList:{
        type:Array,
        default(){
          return[]
        }
      }
    },
  methods:{
    delSong(id){
      this.$emit("delSong",id)
    },
    editSong(id){
      this.$emit("editSong",id)
    }
  }
  }
</script>

<style scoped>
  table{
    width: 100%;
  }

  tr{
    display: flex;

    height: 50px;
    line-height: 50px;
    border-bottom: 1px solid #d3d3d3;
  }
  th,td{
    flex: 1;
    text-align: left;
  }

  .text-red{
    color: red;
  }

  .none-content{
    width: 500px;
    height: 100px;

    position: absolute;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    margin: auto auto;
  }

  .none-text{
    font-size: 25px;
  }

  .list-btn{
    width: 60px;
    height: 30px;

    border-radius: 5px;
    border: 1px solid #707070;
    background-color: #fff;
    margin-right: 20px;
  }

</style>
