<template>
  <!-- <div>{{title}}</div> -->
  <input type="text" :value="title">
</template>

<script>
  export default {
    name: "MyComponents",
    model: {
      prop: 'modelVal',//指向props的参数名
      event: 'change'//事件名称
    },
    props: {
      modelVal:''
    },
    data(){
      return {
        title:''
      }
    },
    watch:{
      //监听值变化，再赋值给modelVal
      title(value){
        this.$emit('change',value);
      }
    }
  }
</script>

<style scoped>

</style>