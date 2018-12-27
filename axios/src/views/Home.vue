<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <h1><span><img :src="test.tag_icon" alt=""></span>{{test.tag_name}}</h1>
    <ul>
      <li v-for="t in test.operation_source_list">
        <p><img :src="t.pic_url" alt=""></p>
      </li>
    </ul>
    <ul>
      <li v-for="(food_spu_tag,index) in food_spu_tags"  >
        <p>
          
          <h2 style="text-align:left"><span><img :src="food_spu_tag.icon" alt="" ></span>  {{food_spu_tag.name}}</h2>
        </p>
        <ul >
          <li v-for="v in food_spu_tag.spus" class="list" >
             <img :src="v.picture" alt="" width="70" height="70">
            <ul class="list1">
              <li class="name">{{v.name}}</li>
              <li class="saled_content">销量：{{v.month_saled_content}}</li>
              <li class="praise_content">评论：{{v.praise_content}}</li>
            </ul>
          </li>
        </ul>
        
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  data(){
    return {
      test:{},
      food_spu_tags:[],
      sups:[],
    }
  },
  components: {
    HelloWorld
  },
  created(){
      this.$axios.get('/api/goods')
     
      .then((data) =>{
        console.log(data.data.data)
        // console.log(data.data.data.food_spu_tags)
        this.test = data.data.data.container_operation_source
        this.food_spu_tags = data.data.data.food_spu_tags
      })
    }
}
</script>
<style scoped>
  .list{list-style: none;display: flex;background: #f4f4f4;margin-bottom: 10px;padding: 10px;}
 li{list-style: none;font-family: Arial, Helvetica, sans-serif}
.list1{text-align: left;}
.name{color: red;font-size: 14px;}
.saled_content{font-weight: bold;padding-top: 5px;padding-bottom: 5px;}
.praise_content{color: #666;font-size: 13px;}
h2{padding-left: 40px;}
</style>
