<script setup lang="ts">
import { CodeEditorLanguage } from '@/types/CodeEditorLanguage';

import CodeEditor from './CodeEditor.vue';

const props = defineProps<{ lang: CodeEditorLanguage }>();

const langToLabelMap = {
  html: 'HTML',
  css: 'CSS',
  javascript: 'JavaScript'
};
const humanisedLabelText = langToLabelMap[props.lang];
const langLabelClass = `lang-${props.lang}`;
</script>

<template>
  <div :class="['editor-label', langLabelClass]">
    <span>{{ humanisedLabelText }}</span>
  </div>
  <div class="editor-container">
    <CodeEditor :lang="props.lang" />
  </div>
</template>

<style scoped>
.editor-container {
  flex: 1 1 auto;
}

.editor-label {
  padding: 4px 0;
  text-align: center;
}

.lang-html,
.lang-css {
  color: #fff;
}

.lang-html {
  background-color: #e54d26;
}

.lang-css {
  background-color: #3799d6;
}

.lang-javascript {
  background-color: #f7df1e;
  color: #000;
}
</style>
