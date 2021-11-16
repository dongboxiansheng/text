<template>
  <div class="container">
    <h1>Todolist</h1>
    <h3>添加新任務</h3>
    <div class="form-group"></div>
    <label for="add"></label>
    <input type="text" placeholder="添加新的todo" class="form-control" v-model="value">
    <button type="button" class="btn btn-primary btn-lg btn-block" @click="add"></button>
    <h3>正在進行</h3>
    <ul class="list-group">
      <template v-for="(item,index) in lists">
        <li class="list-group-item" v-if="!item.checked"  :key="index" @click="()=>item.checked=!item.checked ">
        <div class="form-group form-check">
          <input type="checkbox" class="form-check-input" :id="'item-'+index" v-model="item.checked">
          <label class="form-check-label" :for="'item-'+index">{{item.name}}</label>
        </div>
        </li>
      </template>
    </ul>
    <h3>已完成的</h3>
    <ul class="list-group">
      <li class="list-group-item" v-for="(item,index) in finished" :key="'finished-'+index" >
        <div class="form-group form-check">
          <input type="checkbox" class="form-check-input" :id="'finished-'+index" v-model="item.checked" disabled>
          <label class="form-check-label" :for="'finished-'+index">{{item.name}}</label>
        </div>
        </li>
    </ul>
  </div>
</template>
<script>
import {computed, reactive, toRef, toRefs} from 'vue'
export default {
  name:'Home',
  setup(){
    const add= ()=>{
      state.lists.push({
        name:state.value,
        checked:false,
        isEdit:false,
      })
      state.value=''
    }
    const state = reactive({
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
      finish:computed(()=>state.lists.filter((item)=>item.checked ==true))
    }),
    return toRefs()
  }
   
}
</script>