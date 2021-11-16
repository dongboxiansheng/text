<template>
  <div class="container"></div>
  <h1>Todolist</h1>
  <h3>添加新的todo</h3>
  <div class="form-group">
    <input type="text" placeholder="添加新的todo" id="add" class="form-control" v-model="value" @keydown.enter="add">
  </div>
  <button type="button" class="btn btn-primary btn-lg btn-block" @click="add">確定添加</button>

  <ul class="list-group">
    <template v-for="(item,index) in lists">
      <li class="list-group-item" v-if="!item.checked"  :key="index" @click="()=>item.checked=!item.checked ">
      <div class="form-group form-check" >
        <input type="checkbox" class="form-check-input" :id="'item-'+index" v-model="item.checked">
        <label :for="'item-'+index" class="form-check-label">{{item.name}}</label>
        <button @click="remove(index)">刪除</button>
      </div>
    </li>
    </template>
  </ul>
  <h3>已完成的</h3>
   <ul class="list-group">
    <li  class="list-group-item" v-for="(item,index) in finished" :key="'finished-'+index">
      <div class="form-group form-check">
        <input type="checkbox" class="form-check-input" :id="'finished-'+index" v-model="item.checked" disabled>
        <label :for="'finished-'+index" class="form-check-label">{{item.name}}</label>
      </div>
    </li>
  </ul>
</template>

<script>
import {computed, reactive, toRefs} from 'vue'
export default {
 name:"Home",
 setup(){

   const add =()=>{
     state.lists.push({
       name:state.value,
       checked:false,
       isEdit:false,
     })
     state.value =''
   }
   const remove= (index) =>{
     state.lists.splice(index,1)
   }
   const state = reactive({
     value:'',
     editValue:'',
     lists:[{
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
      ],
      finished:computed(()=>state.lists.filter((item)=>item.checked==true))
   })
   return {...toRefs(state),add,remove}
 }
}
</script>