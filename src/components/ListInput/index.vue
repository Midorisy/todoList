<template>
    <div class="search-main default-style">
        <form>
            <input v-model="text" type="text"> <button type="button" @click="text = ''">清除输入</button><button
                @click="submitItem" type="button">提交</button>
        </form>
    </div>
</template>

<script setup>
import { nanoid } from 'nanoid';
import { ref } from 'vue';
const { ListData } = defineProps({
    ListData: {
        type: Array,
        default: () => []
    }
})
const emit = defineEmits(['emitItem'])

// 创建默认数据
const newItem = ref({})
const text = ref('')

/**
 * 提交整合后的数据
 */
function submitItem() {
    if (text.value.trim().length === 0) {
        return
    }
    newItem.value.text = text.value
    newItem.value.id = nanoid()
    newItem.value.isDone = false
    newItem.value.index = ListData.length
    emit('emitItem', newItem)
    newItem.value = {}
    text.value = ''
}
</script>

<style scoped>
.search-main {
    height: 50px;
    background-color: yellowgreen;
}
</style>