<template>
  <div class="container">
    <GlobalHeader :user="currentUser" />
    <!-- <column-list :list="testData"></column-list> -->
    <validate-form @form-submit="onFormSubmit">
      <div class="mb-3">
        <label class="form-label">邮箱地址</label>
        <validate-input :rules="emailRules" v-model="emailVal" type="text" placeholder="请输入邮箱"></validate-input>
      </div>
      <div class="mb-3">
        <label class="form-label">密码</label>
        <validate-input :rules="emailRules" v-model="emailVal" type="password" placeholder="请输入密码"></validate-input>
      </div>

    </validate-form>
  </div>
</template>


<script setup lang="ts">
import { ref } from 'vue';
import ColumnList from './components/ColumnList.vue';
import ValidateForm from './components/ValidateForm.vue';
import GlobalHeader from './components/GlobalHeader.vue';
import type { ColumnProps } from './components/ColumnList.vue'
import type { UserProps } from './components/GlobalHeader.vue';
import 'bootstrap/dist/css/bootstrap.min.css'
import ValidateInput from './components/ValidateInput.vue';
import type  { RulesProp} from './components/ValidateInput.vue'

const emailVal = ref('')

const emailRules: RulesProp = [
  { type: 'required', message: '电子邮箱地址不能为空' },
  { type: 'email', message: '请输入正确的电子邮箱格式' }
]
const currentUser: UserProps = {
  isLogin: true,
  name: 'george',
  id: 111
}
const onFormSubmit = (result: boolean) => {
  console.log(result)
}
const testData: ColumnProps[] = [
  {
    id: 1,
    title: 'test1的专栏',
    description: '这是的test1专栏，有一段非常有意思的简介，可以更新一下欧',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  },
  {
    id: 2,
    title: 'test2的专栏',
    description: '这是的test2专栏，有一段非常有意思的简介，可以更新一下欧',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  },
  {
    id: 1,
    title: 'test1的专栏',
    description: '这是的test1专栏，有一段非常有意思的简介，可以更新一下欧',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  },
  {
    id: 2,
    title: 'test2的专栏',
    description: '这是的test2专栏，有一段非常有意思的简介，可以更新一下欧',
    avatar: 'http://vue-maker.oss-cn-hangzhou.aliyuncs.com/vue-marker/5ee22dd58b3c4520912b9470.jpg?x-oss-process=image/resize,m_pad,h_100,w_100'
  }
]
</script>

<style></style>