<script setup lang="ts">
import { Ace } from 'ace-builds';
import { VAceEditor } from 'vue3-ace-editor';
import { debounce } from 'debounce';

import { CodeEditorLanguage } from '@/types/CodeEditorLanguage';
import { useCodeStore, Actions } from '@/stores/code';

const props = defineProps<{ lang: CodeEditorLanguage }>();

const codeStore = useCodeStore();
const editorContent = codeStore[props.lang];

const langToActionNameMap = {
  html: 'setHtml',
  css: 'setCss',
  javascript: 'setJavascript'
};

const action = langToActionNameMap[props.lang] as keyof Actions;
const updateCode = debounce(codeStore[action], 500);

const aceEditorOptions: Partial<Ace.EditorOptions> = {
  useWorker: true,
  fontSize: 18,
  tabSize: 2
};
</script>

<template>
  <VAceEditor
    theme="tomorrow"
    :lang="props.lang"
    :options="aceEditorOptions"
    :value="editorContent"
    @update:value="updateCode"
  />
</template>

<style scoped>
.ace_editor {
  width: 100%;
  height: 100%;
}
</style>
