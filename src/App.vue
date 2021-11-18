<template>
  <h1>Todolist</h1>
  <el-form class="demo-ruleForm" >
    <div class="header">
    <el-input v-model="input" placeholder="添加新的todo"  id="add"  @keydown.enter="add" class="input" />
    <!-- <input type="text" placeholder="添加新的todo" id="add" class="form-control" v-model="state.value" @keydown.enter="add"> -->
    <el-button type="primary" @click="add" class="button">添加todo</el-button>
  </div>
   <br>
   <br>
  <Child :state="state" @remove="remove" @change="change" :finished="finished" :count="count" :donecount="donecount"></Child>
  </el-form>
</template>

<script   setup lang="ts">
import Child from './components/Child.vue'
import { reactive,ref,computed} from "vue";
const input =ref<Object>([])
const count = ref<number>(3)
const donecount = ref<number>(0)
const remove= (index) =>{
      count.value--;
     state.lists.splice(index,1)
   }
  const change = ()=>{
    count.value--;
    donecount.value++;
    console.log(finished.value);
  }
  const add = ()=>{
  count.value++;
   state.lists.push({
      name:input.value,
       checked:false,
       isEdit:false,
   })
   state.value =''
}
const state =reactive({
  value:'',
  lists:[
    {
        name :'1',
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
  ],
})
const finished = computed(()=>{
  return state.lists.filter((item)=>item.checked==true)
})

</script>

<style lang="scss">
.header{
  position: relative;
  .input{
    position: absolute;
  }
  .button{
    right: 0px;
    position: absolute;
  }
}
</style>

