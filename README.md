# Popup 功能工具集

本模块提供了一组用于在 Vue 应用中操作弹窗组件的工具函数。

## 功能特性

### 弹窗可见性控制

- `usePopupVisible()` - 获取当前弹窗组件的可见状态（`Ref<boolean>`）
- `usePopupMethods()` - 获取弹窗的确认和关闭方法
- `usePopupAll()` - 获取弹窗的所有状态和方法（可见性 + 操作方法）

### 函数式组件处理

- `useFunctionComponent()` - 用于操作函数式组件的工具，接受组件及其 props 作为参数

### 插件管理

- `setPlugin()` - 设置 Vue 插件

### 调用示例

```vue
<!-- 弹框组件 Popup.vue -->
<template>
  <div v-if="visible">
    <div>show commit</div>
    <button @click="onFormSubmit">确认</button>
    <button @click="close">取消</button>
  </div>
</template>
<script setup lang="ts">
import { usePopupVisible, usePopupMethods } from '@stardev/fn-component-gen'

const visible = usePopupVisible()
const { close, confirm } = usePopupMethods()

function onFormSubmit(){
    confirm({ data: {} })
}
```

```vue
<template>
  <div>
    <button @click="openPopup">打开弹窗</button>
  </div>
</template>

<script setup lang="ts">
import { useFnComponent } from "@stardev/fn-component-gen";

const openPopup = async () => {
  useFnComponent({
    component: await import("./Popup.vue"),
    props: {},
  }).then((result) => {
    // 弹框调用confirm 返回的结果
    console.log(result);
  });
};
</script>
```
