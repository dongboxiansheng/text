<template>
<el-card class="box-card">
  <div class="card-header">
    <h3>正在进行 <span>{{props.count}}</span></h3>
        <ul class="list-group">
       <template v-for="(item,index) in state.lists">
      <li class="list-group-item" v-if="!item.checked"  :key="index">
      <div class="form-group form-check" >
        <input type="checkbox" class="form-check-input" :id="'item-'+index" v-model="item.checked" @click="change">
        <label :for="'item-'+index" class="form-check-label">{{item.name}}</label>
        <el-button type="danger" @click="remove(index)">删除</el-button>
      </div>
    </li>
    </template>
        </ul>
    <h3>已完成的 <span>{{props.donecount}}</span></h3>
   <ul class="list-group">
    <li  class="list-group-item" v-for="(item,index) in finished" :key="'finished-'+index">
      <div class="form-group form-check">
        <input type="checkbox"  :id="'finished-'+index" v-model="item.checked" disabled>
        <label :for="'finished-'+index" >{{item.name}}</label>
      </div>
    </li>
  </ul>
      </div>
</el-card>
</template>

<script setup>
import { defineProps,defineEmits } from 'vue'
const props=defineProps({
  state:{
    type:Array,
    require:true
  },
  count:{
    type:Number,
    require:true
  },
  donecount:{
    type:Number,
    require:true
  },
  finished:{
    type:Array,
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
 console.log(props.state)
</script>