<script setup>
// 自定义属性
defineProps({
  isAllChecked:Boolean, // 是否全选
  allMoney:{
    type:Number,default:0 // 总金额
  },
  allCount:{
    type:Number,default:0 // 总个数
  }
})

// 自定义事件
let emits = defineEmits([
  'changeAllCheckedState'
])
</script>

<template>
    <div class="container">
      <div class="selection">
        <label>
            <input type="checkbox" class="select-all" 
            :checked="isAllChecked" @change="emits('changeAllCheckedState',$event.target.checked)">
            <span>全选</span>
        </label>
      </div>
      <span>
        合计金额:<strong>￥ {{ allMoney }}</strong>
      </span>
      <button>
        结算[{{ allCount }}]
      </button>
    </div>
  </template>

<style>
.container{
    padding: 20px;
    margin: auto 15px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.container input{
    width:15px;
    height:15px;
}
.container label{
    display: flex;
    align-items: center;
    width: 70px;
    justify-content: space-between;
}
.container strong{
    color:red;
    font-size: 25px;
}

.container button {
    border:none;
    padding:15px 25px;
    background-color: blue;
    color: white;
    border-radius: 8px;
    box-shadow: 0 0 5px gray;
}
</style>