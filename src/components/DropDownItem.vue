<template>
  <li
    class="dropdown-option"
    :class="{'is-disabled': disabled}"
  >
    <slot></slot>
  </li>
</template>

<script setup lang="ts">
const props = defineProps({
    disabled: {
        type: Boolean,
        default: false
    }
})
const disabled = props.disabled
</script>

<style>
.dropdown-option.is-disabled * {
  color: #6c757d;
  pointer-events: none;
  background-color: transparent;
}
</style>