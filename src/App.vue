<script setup>
import { ref } from 'vue';
import ProductVue from './components/Product.vue';
import Collection from './components/Collection.vue';
import { computed } from 'vue';
// 购物车
let shopCar = ref([
  {
    id:89,
    title:'蒲恋正宗蒙阴黄桃【多地次日达】 桃子新鲜水果礼盒当季时令生鲜 源头直采【性价比高】 净重4.5斤装【单果125g+】中果',
    subtitle:'由蒲恋生鲜旗舰店发货, 并提供售后服务. 现在下单，承诺7月25日24:00前发货，预计7月27日24:00前送达',
    image:'https://img11.360buyimg.com/n7/jfs/t1/185638/36/46468/166803/6670ed35Fff63409b/4d6c99b16d55cd0d.jpg',
    price:9.9,
    count:1,
    selected:false
  },
  {
    id:102,
    title:'华北强（HUABEIQIANG）【限量亏本500件 抢到就是赚到】山西水蜜桃子新鲜水果毛整箱批发 水蜜桃带箱5斤装净重4.5-5斤',
    subtitle:'此商品为预订商品，下单后在07月23日至07月27日发货',
    image:'https://img14.360buyimg.com/n7/jfs/t1/113764/32/28395/140523/628b02ecE34141af7/9fe284ff0effa285.jpg',
    price:18.80,
    count:1,
    selected:true
  },
  {
    id:108,
    title:'京鲜生 民勤蜜瓜 3-4粒装 净重8-10斤 生鲜水果 源头直发',
    subtitle:'由 供应商 发货, 并提供售后服务.',
    image:'https://img13.360buyimg.com/n1/jfs/t1/246454/19/12647/83233/667d308fF8f148e2d/6aa12b5c4bc23420.png.avif',
    price:19.90,
    count:1,
    selected:false
  }
])
//产品的状态发生改变的方法
function changeShopCarProductChecked(checked, id){
  shopCar.value.some(product=>{
    if(id === product.id){
      product.selected = checked
      return true
    }
  })
}

// 产品数量更改
function changeShopCarProductCount(count,id){
    shopCar.value.some(product=> {
      if(id === product.id){
        product.count += count;
        return true;
      }
    })
}

// 是否全选
let isFullSelectProduct = computed(()=>{
  return shopCar.value.every(product => product.selected)
})

// 改变购物车所有产品篇的选中状态
function changeAllShopCarProductCheckedState(checked){
  shopCar.value.forEach(product =>
    product.selected = checked    
  )
}

// 总金额
let total = computed(()=>{
  return shopCar.value
  .filter(item =>item.selected)// 过滤掉被选中的产品
  .reduce((money,item)=>(money += item.price * item.count),0)
})

// 购买总数量
let countsum = computed(()=>{
  return shopCar.value 
  .filter(item => item.selected)
  .reduce((count,item)=>(count += item.count),0)
})
</script>

<template>
  <ProductVue 
  v-for="product in shopCar" 
  :key="product.id"
  :id="product.id" 
  :picture="product.image"
  :title="product.title"
  :subtitle="product.subtitle"
  :price="product.price"
  :count="product.count"
  :is-checked="product.selected"
  @change-product-checked="changeShopCarProductChecked"
  @change-product-count="changeShopCarProductCount"/>

  <hr>
  <Collection :is-all-checked="isFullSelectProduct"
  :all-money="total"
  :all-count="countsum"
  @change-all-checked-state="changeAllShopCarProductCheckedState"/>
</template>

<style>
  *{
    margin:0;
    padding:0;
  }
</style>