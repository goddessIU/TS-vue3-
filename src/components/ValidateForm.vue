<template>
    <form action="validate-form-container">
        <slot name="default"></slot>
        <div class="submit-area" @click.prevent="submitForm">
            <slot name="submit">
                <button type="submit" class="btn btn-primary">提交</button>
            </slot>
        </div>
    </form>
</template>


<script lang="ts" setup>
import mitt from 'mitt';
import { onUnmounted } from 'vue';
type ValidateFunc = () => boolean
const emitter = mitt()

const funcArr: ValidateFunc[] = []
const emit = defineEmits(['form-submit'])
const submitForm = () => {
    const result = funcArr.map(func => func()).every(result => result)
    emit('form-submit', result)
}
const callback = (func: ValidateFunc) => {
    funcArr.push(func)
}
emitter.on('form-item-created', callback)
onUnmounted(() => {
    emitter.off('form-item-created', callback)
    funcArr = []
})
</script>