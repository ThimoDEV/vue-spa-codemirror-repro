<script setup lang="ts">
import Test from './components/Test.vue'
import { ref, onMounted, watchEffect } from 'vue'
import { javascript } from '@codemirror/lang-javascript'
import type { ViewUpdate } from '@codemirror/view'

const code = ref('console.log("Hello, CodeMirror!");')
const theme = ref<'light' | 'dark' | 'none'>('none')
const codemirror = ref<CodeMirrorRef>()

const handleChange = (value: string, viewUpdate: ViewUpdate) => {
  console.log('Value changed:', value)
  console.log('View updated:', viewUpdate)
}

const handleStatistics = (stats: Statistics) => {
  console.log('Editor statistics:', stats)
}

const handleUpdate = (viewUpdate: ViewUpdate) => {
  console.log('Editor updated:', viewUpdate)
}

onMounted(() => {
  if (codemirror.value) {
    console.log('Log editorRef', codemirror.value.editor)
    console.log('Log containerRef', codemirror.value.container)
  }

  watchEffect(() => {
    if (codemirror.value) {
      console.log('Log StateRef', codemirror.value.state)
      console.log('Log viewRef', codemirror.value.view)
    }
  })
})
</script>

<template>
  <div>
    <Test
    ref="codemirror"
    v-model="code"
    :theme="theme"
    style="width: 500px; height: 400px;"
    placeholder="Enter your code here..."
    :auto-focus="true"
    :editable="true"
    :extensions="[javascript()]"
    :basic-setup="true"
    :indent-with-tab="true"
    @on-change="handleChange"
    @statistics="handleStatistics"
    @on-update="handleUpdate"
  />
  </div>
</template>
