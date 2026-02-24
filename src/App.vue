<template>
  <div class="main default-style">
    <keep-alive>
      <list-mask @close-mask="maskCloseEvent" @is-confirm="deleteData" v-if="isOpen"></list-mask>
    </keep-alive>
    <list-head></list-head>
    <list-input :ListData="ListData" @emit-item="reciveItem"></list-input>
    <list-body :ListData="ListData"></list-body>
    <list-bottom @clear-item="openMask" :ListData="ListData"></list-bottom>
  </div>
</template>

<script setup>
import ListHead from "./components/ListHead/index.vue";
import ListInput from "./components/ListInput/index.vue";
import ListBody from "./components/ListBody/index.vue";
import ListBottom from "./components/ListBottom/index.vue";
import ListMask from './components/ListMask/index.vue'
import { ref, provide } from "vue";

// 初始化待办数据
const ListData = ref([
  {
    text: '要待办的事情1',
    isDone: false,
    id: '001',
    index: 0
  },
  {
    text: '要待办的事情2，已完成时会有特别的样式',
    isDone: true,
    id: '002',
    index: 1
  }
])

const isOpen = ref(false)

/**
 * 接收Input组件传入的单个数据
 */
function reciveItem(item) {
  ListData.value.push(item.value)
  console.log(ListData.value);
}

/**
 * 根据index删除某一项的函数
 * @param index item项的index
 */
function deleteItemCb(index) {

  ListData.value.splice(index, 1)
}
// 给子组件提供数据
provide('childrenCb', deleteItemCb)

/**
 * 打开遮罩层
 */
function openMask() {
  isOpen.value = true

}

/**
 * 关闭遮罩层
 * @param {boolean} flag 为真时开启遮罩层
 */

function maskCloseEvent(flag) {
  isOpen.value = flag
}

/**
 * 删除数据的函数
 * @param {boolean} flag  为真时删除已完成
 */
function deleteData(flag) {
  if (flag) {
    ListData.value = ListData.value.filter((item) => {
      return item.isDone !== true
    })
  } else {
    console.log(flag);
    ListData.value = []
  }
}
</script>

<style scoped>
/* 最外层边框 */
.main {
  position: relative;
  display: flex;
  flex-direction: column;
  margin: 30px auto;
  width: 400px;
  height: 500px;
  box-shadow: 0 0 5px 5px #ccc;
  padding: 10px;
}

div[data-v-7ba5bd90] {
  margin-bottom: 10px;

  &:last-child {
    margin-bottom: 0px;
  }
}
</style>
