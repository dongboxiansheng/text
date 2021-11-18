<template>
<el-form class="demo-ruleForm">
<div class="card-header">
    <h3>正在进行 <span>{{finishing.length}}</span></h3>
        <el-scrollbar max-height="150px">
           <ul>
      <li v-for="(item,index) in finishing" :key="index">
      <div class="form-group form-check" >
        <el-checkbox v-model="item.checked" :id="'item-'+index" @click="change">
        <label :for="'item-'+index" class="form-check-label">{{item.name}}</label>
        </el-checkbox>
        <!-- <input type="checkbox" class="form-check-input" :id="'item-'+index" v-model="item.checked" @click="change">
        <label :for="'item-'+index" class="form-check-label">{{item.name}}</label> -->
        <el-button type="danger" @click="remove(index)">删除</el-button>
      </div>
    </li>
    
        </ul>
        </el-scrollbar>
      <h3>已完成的 <span>{{finished.length}}</span></h3>
        <ul>
    <li  v-for="(item,index) in finished" :key="'finished-'+index">
      <div class="form-group form-check">
        <el-checkbox v-model="item.checked" :id="'finished-'+index" >
        <label :for="'finished-'+index" >{{item.name}}</label>
        </el-checkbox>
      </div>
    </li>
  </ul>
      </div>
</el-form>
</template>

<script setup lang="ts">

import { defineProps,defineEmits } from 'vue'
const props=defineProps({
  state:{
    type:Object,
    require:true
  },
  finished:{
    type:Object,
    require:true
  },
  finishing:{
    type:Object,
    require:true
  }
})
const emit =defineEmits([
  'remove','change'
])
const remove =(index)=>{
  emit('remove',index)
}
const change = ()=>{
  emit('change')
}
 console.log(props.state.lists)
 
</script>

<style>
ul{
  list-style:none ;
}
</style>