<template>
    <div class="default-style body-main">
        <div class="haveData" v-if="ListData.length !== 0">
            <todo-item :itemData="item" :itemIndex="index" v-for="(item, index) in ListData" :key="item.id"></todo-item>
        </div>
        <div class="noData" v-else>
            没有任何数据
        </div>
    </div>
</template>

<script setup>
import TodoItem from "./TodoItem/index.vue";

const { ListData } = defineProps({
    ListData: {
        type: Array,
        default: () => []
    }
})
</script>

<style scoped>
.body-main {
    width: 100%;
    background-color: skyblue;
}
</style>