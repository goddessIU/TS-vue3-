<template>
    <nav class="navbar navbar-dark bg-primary justify-content-between mb-4 px-4">
    <a class="navbar-brand" href="#">者也专栏</a>
    <ul v-if="!user.isLogin" class="list-inline mb-0">
      <li class="list-inline-item"><a href="#" class="btn btn-outline-light my-2">登陆</a></li>
      <li class="list-inline-item"><a href="#" class="btn btn-outline-light my-2">注册</a></li>
    </ul>
    <ul v-else class="list-inline mb-0">
      <li class="list-inline-item">
          <DropDown :title="user.name || ' '"> 
            <DropDownItem>编辑文档</DropDownItem>
            <DropDownItem disabled>编辑文档</DropDownItem>
            <DropDownItem>编辑文档</DropDownItem>
          </DropDown>
      </li>
    </ul>
  </nav>
</template>

<script lang="ts" setup>
import DropDown from './DropDown.vue';
import DropDownItem from './DropDownItem.vue';
import type { PropType } from 'vue';

export interface UserProps {
    isLogin: boolean;
    name?: string;
    id?: number;
}
const props = defineProps({
    user: {
        type: Object as PropType<UserProps>,
        required: true
    }
})
const user = props.user;
</script>