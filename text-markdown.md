mark-down-test
test
| Tables | Are | Cool |
| :-------: | :----:| :----:|
| col 3 is | right-aligned | $1600|
| col 2 is | centered | $12 |
| zebra stripes | are neat | $1 |

## 自定义容器

> 自定义容器可以通过他们的类型、标题喝内容来定义。

::: info
This is an info box.
:::

::: tip
This is a tip.
:::

::: warning
This is a warning
:::

::: danger
This is a dangerous warning
:::

::: details
This is a details block
:::

## 自定义标题

::: details 点我查看代码

```js
console.log("hello vitepress");
```

:::

::: danger STOP
危险区域，请勿继续
:::

### 代码块中聚焦

```js
export default {
  data() {
    return {
      msg: "Focused!", // [!code focus]
    };
  },
};
```

### 代码块中实现高亮

输入

```js{4}
export default {
  data() { // [!code highlight]
    return {
      msg: "Highlighted!",
    };
  },
};
```

### 代码块中的颜色高亮

```js
export default {
  data() {
    return {
      msg: "Removed", // [!code --]
      msg: "add", // [!code ++]
    };
  },
};
```

### 高亮显示错误和警告

```js
export default {
  data() {
    return {
      msg: "警告", // [!code warning]
      msg: "错误", // [!code error]
    };
  },
};
```

### 行号

```js:line-numbers{1}
export default{
  data(){
    return {
      msg: 'msg'
    }
  }
}
```

### 代码分组

::: code-group

```js [config.js]
export default {
  data() {
    return {
      msg: "我是js的config.js",
    };
  },
};
```

```ts [config.ts]
import type { UserConfig } from "vitepress";
const config: UserConfig = {
  //
};
/**
 *
 *
 */
export default {
  data() {
    return {
      msg: "我是ts",
    };
  },
};
```

:::

### 代码块中不转义

> 默认情况下，代码是受到保护的，都会自动使用 `v-pre` 包装，因此内部不会处理任何
> Vue 语法。要在代码块内启用 Vue 插值语法，可以在代码语言后附加`-vue`后缀，例如`js-vue`：

#### 输入

```js-vue

Hello {{ 1+1}}
nihao
```

## 使用 teleport 传递组件内容

> VitePress 目前只有使用 TELEPORT 传送到 body 的 SSG 支持。对于其他地方，可以将他们包裹在内置的`<ClientOnly>`组件中，或者通过 <mark><u>postRender 钩子</u></mark>将 teleport 标签注入到最终页面 HTML 中的正确位置。

::: details 点开我是代码块

```ts
<script setup lang="ts">
import { ref } from 'vue'
const showModal = ref(false)
</script>

<template>
  <button class="modal-button" @click="showModal = true">Show Modal</button>

  <Teleport to="body">
    <Transition name="modal">
      <div v-show="showModal" class="modal-mask">
        <div class="modal-container">
          <p>Hello from the modal!</p>
          <div class="model-footer">
            <button class="modal-button" @click="showModal = false">
              Close
            </button>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<style scoped>
.modal-mask {
  position: fixed;
  z-index: 200;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: opacity 0.3s ease;
}

.modal-container {
  width: 300px;
  margin: auto;
  padding: 20px 30px;
  background-color: var(--vp-c-bg);
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.model-footer {
  margin-top: 8px;
  text-align: right;
}

.modal-button {
  padding: 4px 8px;
  border-radius: 4px;
  border-color: var(--vp-button-alt-border);
  color: var(--vp-button-alt-text);
  background-color: var(--vp-button-alt-bg);
}

.modal-button:hover {
  border-color: var(--vp-button-alt-hover-border);
  color: var(--vp-button-alt-hover-text);
  background-color: var(--vp-button-alt-hover-bg);
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  transform: scale(1.1);
}
</style>

```

:::
