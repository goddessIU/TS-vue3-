<template>
    <div class="validate-input-container pb-3">
        <input
            class="form-control"
            :class="{ 'is-invalid': inputRef.error }"
            :value="inputRef.val"
            @blur="validateInput"
            @input="updateValue"
             v-bind="$attrs"
        />
        <span v-if="inputRef.error" class="invalid-feedback">{{ inputRef.message }}</span>
    </div>
</template>


<script lang="ts">
// use normal <script> to declare options
export default {
  inheritAttrs: false
}
</script>
<script setup lang="ts">
import { onMounted, reactive, type PropType } from 'vue';

import {emitter} from './ValidateForm.vue'

onMounted(() => {
    emitter.emit('form-item-created', inputRef.val)
})
interface RuleProp {
    type: 'required' | 'email';
    message: string;
}
type RulesProp = RuleProp[]
const emit = defineEmits(['update:modelValue'])

const emailReg = /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/

const props = defineProps({
    rules: Array as PropType<RulesProp>,
    modelValue: String
})

const inputRef = reactive({
    val: props.modelValue || '',
    error: false,
    message: ''
})
const updateValue = (e: KeyboardEvent) => {
    const targetValue = (e.target as HTMLInputElement).value
    inputRef.val = targetValue
    emit('update:modelValue', targetValue)
}
const validateInput = () => {
    if (props.rules) {
        const allPassed = props.rules.every(rule => {
            let passed = true;
            inputRef.message = rule.message;
            switch (rule.type) {
                case 'required':
                    passed = (inputRef.val.trim() !== '')
                    break
                case 'email':
                    passed = (emailReg.test(inputRef.val))
                    break
                default:
                    break
            }
            return passed
        })
        inputRef.error = !allPassed
    }
}

</script>