<template>
    <ul v-if="isComplete > 0">
       <li v-for="(item, index) in props.list " :key="index" class="item" >
        <input  type="checkbox" > {{item.title}}
        <button @click="sonFn" class="RefChilde" >删除</button>
       </li>
   </ul>
</template>

<script setup>
    import { computed, defineProps} from "vue";
    const props = defineProps({
     list: {
       type: Array
     }
    })
    let isComplete = computed(()=>{
    let arr = props.list.filter(item => {
    return item.checked
    })
      return arr.length
    })
</script>

<style lang="scss" scoped>
.RefChilde{
   margin-left: 600px;
  border-radius: 15px;}
</style>