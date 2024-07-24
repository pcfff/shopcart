<script setup>
// 声明组件的自定义属性
let props = defineProps({
    id:{type:Number,required:true},
    isChecked:Boolean,
    picture:{type:String,required:true},
    title:{type:String,required:true},
    subtitle:{type:String,required:true},
    price:{type:Number,default:0},
    count:{type:Number,default:0}
})


let emits = defineEmits([
    'changeProductChecked', // 改变复选框的状态事件
    'changeProductCount'
])
// 改变产品选中的状态
function changeCheckedSate(e){
    let newCheckeState = e.target.checked // 复选框最新的状态
    emits('changeProductChecked',newCheckeState,props.id) // 触发自定义的事件,并传值给父组件
}
</script>


<template>
    <!-- 产品容器 -->
    <div class="box">
        <!-- 选项框 -->
        <input type="checkbox" class="p_checkbox" :checked="isChecked" @change="changeCheckedSate">
        <!-- 产品图 -->
        <img class="p_img" :src="picture">
        <!-- 产品内容 -->
        <div class="p_content">
            <h3 class="p_title">{{ title }}</h3>
            <!-- 副标题 -->
            <span class="p_subtitle">{{subtitle}}</span>
            <!-- 价格 -->
            <h2 class="p_price">￥{{ price }}</h2>
            <!-- 产品数量区域 -->
            <div class="p_count_area">
                <button :disabled="count<=1" @click="emits('changeProductCount',-1,props.id)">-</button>
                <span>{{ count }}</span>
                <button @click="emits('changeProductCount',1,props.id)">+</button>
            </div>
        </div>
    </div>
</template>

<style>
    .box{
        box-shadow: 0 0 8px grey;
        padding: 20px;
        margin: 15px;
        display: flex;
        align-items: center;
    }
    .p_checkbox{
        width: 25px;
        height: 25px;
    }
    .p_img{
        width: 200px;
        height: 200px;
        margin: 0px 20px;
    }
    .p_content{
        align-self: start;
        position: relative;
        width: 100%;
    }
    .p_title{
        margin-bottom:8px;
    }
    .p_subtitle{
        font-size: 14px;
        color:grey;
    }
    .p_price{
        margin-top: 150px;
        color: red;
        font-size: 35px;
    }
    .p_count_area button{
        width:25px;
        height:25px;
    }

    .p_count_area span{
        margin: 0 10px;
    }
    .p_count_area {
        position:absolute;
        bottom:0;
        right:0;
    }
</style>