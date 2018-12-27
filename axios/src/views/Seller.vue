<template>
  
</template>
<script>
export default{
  data(){
    return{

    }
  },
  created(){
    this.$axios.get("/api/seller")
    .then((data) => {
      console.log(data)
    })
  }
}
</script>
