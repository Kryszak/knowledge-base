<template>
  <div class="markdown-content" v-if="html" v-html="html"></div>

  <div v-else-if="loading">Loading...</div>

  <div v-else-if="error">
    {{ error }}
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'
import { marked } from 'marked'

const props = defineProps({
  file: {
    type: String,
    required: true,
  },
})

const html = ref('')
const loading = ref(false)
const error = ref('')

async function loadMarkdown(file) {
  loading.value = true
  error.value = ''
  html.value = ''

  try {
    const response = await fetch(file)

    if (!response.ok) {
      throw new Error(`Failed to load markdown (${response.status})`)
    }

    const markdown = await response.text()
    html.value = marked.parse(markdown)
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
}

watch(
  () => props.file,
  (newFile) => {
    if (newFile) loadMarkdown(newFile)
  },
  { immediate: true },
)
</script>

<style scoped>
.markdown-content {
  line-height: 1.6;
}

.markdown-content :deep(pre) {
  overflow-x: auto;
}

.markdown-content :deep(code) {
  font-family: monospace;
}
</style>
