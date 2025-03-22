<template>
  <h1 class="green">{{messageHello}}</h1>
</template>

<script>
export default {

    // props:['message']
    props:{
        messageHello:{
            require:true,
            type:String
        }
    }
}
</script>

<style scoped>
.green {
  color: rgb(38, 170, 38);
}
</style>