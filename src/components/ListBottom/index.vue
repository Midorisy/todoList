<template>
    <div class="bottom-main default-style">
        已完成({{ isDoneCount }}) / 全部({{ allCount }})
        <button @click="clearItem">清空所有任务</button>

    </div>
</template>

<script setup>
import { computed, ref } from 'vue';
const { ListData } = defineProps({
    ListData: {
        type: Array,
        default: () => []
    }
})
const emit = defineEmits(['clearItem'])
const isDoneCount = computed(() => {
    return ListData.filter(item => {
        return item.isDone === true
    }).length
})
const allCount = computed(() => ListData.length)
function clearItem() {
    emit('clearItem')
}
</script>

<style scoped>
.bottom-main {
    height: 50px;
    background-color: bisque;
    margin-top: auto;
}
</style>