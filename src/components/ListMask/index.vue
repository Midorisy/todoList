<template>
    <div class="mask" id="mask">
        <div class="innerMask">
            <div class="title">确认删除全部任务？</div>
            <div class="del-done">
                <label for="delData">
                    <input type="checkbox" id="delData" v-model="clearFinish"><span>仅删除已完成数据</span>
                </label>
            </div>
            <button class="cancel" @click="cancelBtn">取消</button><button class="confirm" @click="confirmBtn">确认</button>
        </div>
    </div>

</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['closeMask', 'isConfirm'])
const clearFinish = ref(true)
function changeOpenStatus() {
    emit('closeMask', false)
}

/**
 * 点击取消按钮
 */
function cancelBtn() {
    changeOpenStatus()
}
/**
 * 点击确认按钮，清空任务
 */
function confirmBtn() {
    changeOpenStatus()
    emit('isConfirm', clearFinish.value)
}
</script>

<style scoped>
.mask#mask {
    position: absolute;
    width: 100%;
    height: 100%;
    left: 0;
    top: 0;
    background-color: rgba(0, 0, 0, .3);
    margin-bottom: 0px;
    border-radius: 4px;

    .innerMask {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);
        width: 150px;
        height: 150px;
        background-color: #fff;
        font-size: 14px;
        padding: 10px;
        box-sizing: border-box;
        /* 开始设置gird布局 */
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        grid-template-rows: repeat(3, 1fr);
        align-items: center;
        justify-items: center;

        /* gap: 10px; */
        .title {
            grid-column: span 2;
        }

        .del-done {
            grid-column: 1/3;
        }

        .cancel,
        .confirm {
            align-self: self-end;
        }
    }
}
</style>
