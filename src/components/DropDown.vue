<template>
    <div class="dropdown" ref="dropdownRef">
        <a href="#" class="btn btn-outline-light my-2" @click="toggleOpen">你好 {{title}}</a>
        <ul class="dropdown-menu" :style="{display: 'block'}" v-if="isOpen">
            <slot></slot>
        </ul>
    </div>
</template>

<script lang="ts" setup>
// import { watch } from 'fs';
import { watch, ref, watchEffect } from 'vue';
import useClickOutSide from '../hooks/useClickOutSide';
const props = defineProps({
    title: {
        type: String,
        required: true
    }
})

const dropdownRef = ref<null | HTMLElement>(null)
const isClickOutSide = useClickOutSide(dropdownRef);
const isOpen = ref(false)
const toggleOpen = () => {
    isOpen.value = !isOpen.value;
}
watch(isClickOutSide,  () => {
    if (isClickOutSide.value && isOpen.value) {
        isOpen.value = false;
    }
})
</script>