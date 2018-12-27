<template>
  <div class="about">
    <h1>This is an about page</h1>
    <h1>评价</h1>
    <ul>
      <li>
        <span v-for="comment_score_type_info in comment_score_type_infos">
          <b>{{comment_score_type_info.comment_score_title}}:&nbsp;</b>
          <span style="color:red">&nbsp;{{comment_score_type_info.total_count}}&nbsp;&nbsp;</span>   
        </span>
        <p>
          <span v-for="tab in tabs">
            <b>{{tab.comment_score_title}}：</b>
            <span style="color:red">{{tab.total_count}}&nbsp;&nbsp;</span>
          </span>
        </p>
        
      </li>
      <li v-for="comment in comments" class="list">
        <img :src="comment.user_pic_url" alt=""  width="70" height="70">
        <ul class="list1">
          <li class="name">{{comment.user_name}}</li>
          <li class="comment">{{comment.comment}}</li>
          <li class="food_top">##{{comment.praise_food_tip}}</li>
        </ul>
        <!-- <p>{{comment.user_name}}</p><br>
        <p>{{comment.comment}}</p><br>
        <h6>{{comment.praise_food_tip}}</h6> -->
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name:"about",
  data(){
    return{
      tabs:[],
      comment_score_type_infos:[],
      comments:[]
    }
  },
  created(){
    this.$axios.get("/api/ratings")
    .then((data) =>{
      console.log(data.data.data)
      this.comment_score_type_infos = data.data.data.comment_score_type_infos
      this.comments = data.data.data.comments
      this.tabs = data.data.data.tab
    })
  }
}
</script>
<style scoped>
 .list{list-style: none;display: flex;background: #f4f4f4;margin-bottom: 10px;padding: 10px;}
 li{list-style: none;font-family: Arial, Helvetica, sans-serif}
.list1{text-align: left;}
.name{color: red;font-size: 14px;}
.comment{font-weight: bold;padding-top: 5px;padding-bottom: 5px;}
.food_top{color: #666;font-size: 13px;}
</style>
