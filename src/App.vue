<template>
  <h1>Todolist</h1>
  <h3>添加新的todo</h3>
  <div class="form-group">
    <input type="text" placeholder="添加新的todo" id="add" class="form-control" v-model="value" @keydown.enter="add">
    <el-button type="primary" @click="add">添加todo</el-button>
  </div>
  <Child :state="state" @remove="remove" @change="change" :finished="finished" :count="count" :donecount="donecount"></Child>
</template>

<script setup>
import Child from './components/Child.vue'
import { reactive,ref,computed} from "vue";
const count = ref(3)
const donecount = ref(0)
const remove= (index) =>{
      count.value--;
     state.lists.splice(index,1)
   }
  const change = ()=>{
    donecount.value++;
    count.value--;
  }
  const add = ()=>{
  count.value++;
   state.lists.push({
      name:state.value,
       checked:false,
       isEdit:false,
   })
   state.value =''
}
const state =reactive({
  value:'',
  lists:[
    {
        name:'1',
        checked:false,
        isEdit:false
      },
      {
        name:'2',
        checked:false,
        isEdit:false
      },
      {
        name:'3',
        checked:false,
        isEdit:false
      } 
  ]
})
const finished = computed(()=>{
  return state.lists.filter((item)=>item.checked==true)
})
</script>

