<template>
    <div class="item-main">
        <input type="checkbox" name="isDone" v-model="itemData.isDone">
        <span :class="{ isdone: itemData.isDone }">{{ itemData.text }}</span>
        <button type="button" @click="deleteItem(itemIndex)">删除</button>
    </div>
</template>

<script setup>
import { inject } from 'vue';

const { itemData, itemIndex } = defineProps({
    itemData: {
        type: Object,
        default: () => ({})
    },
    itemIndex: {
        type: Number,
        default: 0
    }
})
// 得到父组件提供的回调函数
const onChildrenEvent = inject('childrenCb')

/**
 * 删除对应的数据
 */
function deleteItem(itemIndex) {
    // 得到点击删除时选中的项目index
    //收到祖先组件提供的回调函数,传递index
    onChildrenEvent(itemIndex)
}
</script>

<style scoped>
.item-main {
    .isdone {
        text-decoration: line-through;
        color: #666;
    }
}
</style>