<template>
  <el-container>
  <el-header>
  <h1>Todolist</h1>
  <h3>添加新的todo</h3>
  <div class="form-group">
    <input type="text" placeholder="添加新的todo" id="add" class="form-control" v-model="value" @keydown.enter="add">
    <el-button type="primary" @click="add">添加todo</el-button>
  </div>
  </el-header>
  <el-main>
  <h3>正在进行 <span>{{count}}</span></h3>
  <ul class="list-group">
    <template v-for="(item,index) in state.lists">
      <li class="list-group-item" v-if="!item.checked"  :key="index" @click="()=>item.checked=!item.checked ">
      <div class="form-group form-check" >
        <input type="checkbox" class="form-check-input" :id="'item-'+index" v-model="item.checked" @click="change">
        <label :for="'item-'+index" class="form-check-label">{{item.name}}</label>
        <el-button type="danger" @click="remove(index)">删除</el-button>
      </div>
    </li>
    </template>
  </ul>
    <h3>已完成的 <span>{{donecount}}</span></h3>
   <ul class="list-group">
    <li  class="list-group-item" v-for="(item,index) in finished" :key="'finished-'+index">
      <div class="form-group form-check">
        <input type="checkbox" class="form-check-input" :id="'finished-'+index" v-model="item.checked" disabled>
        <label :for="'finished-'+index" class="form-check-label">{{item.name}}</label>
      </div>
    </li>
  </ul>
  </el-main>
  </el-container>
</template>

<script setup>

import { reactive,ref,computed} from "vue";

const count = ref(3)
const donecount = ref(0)
const add = ()=>{
  count.value++;
   state.lists.push({
      name:state.value,
       checked:false,
       isEdit:false,
   })
   state.value =''
}
const remove= (index) =>{
      count.value--;
     state.lists.splice(index,1)
   }
  const change = ()=>{
    donecount.value++;
    count.value--;
  }
const state =reactive({
  value:'',
  editValue:'',
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

