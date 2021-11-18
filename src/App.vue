<template>
  <h1>Todolist</h1>
  <el-form class="demo-ruleForm" >
    <div class="header">
    <el-input v-model="input" placeholder="添加新的todo"  id="add"  @blur="add" class="input" />
    <!-- <input type="text" placeholder="添加新的todo" id="add" class="form-control" v-model="state.value" @keydown.enter="add"> -->
    <el-button type="primary" @click="add" class="button">添加todo</el-button>
  </div>
   <br>
   <br>
  <Child :state="state" @remove="remove"  :finished="finished" :count="count" :donecount="donecount" :finishing="finishing"></Child>
  </el-form>
</template>

<script   setup lang="ts">
import Child from './components/Child.vue'
import { reactive,ref,computed} from "vue";
const input =ref<Object>([])
// const info:[string,number,boolean]
// const count =info[2]
// const 
const count = ref<number>(3)
const donecount = ref<number>(0)
const remove= (index) =>{
      // count.value--;
     state.lists.splice(index,1)
   }
  // const change:any = ()=>{
  //   count.value--;
  //   donecount.value++;
  //   console.log(finished.value);
  // }

  const add:any = ()=>{
  count.value++;
   state.lists.push({
      name:input.value,
       checked:false,
       isEdit:false,
   })
   state.value =''
}
const state:any =reactive({
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
const finishing =computed(()=>{
  return state.lists.filter((item)=>item.checked==false)
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

