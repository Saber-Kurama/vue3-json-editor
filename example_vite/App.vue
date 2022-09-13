<template>
  <div class="example-json">
    <div class="example-demo">vue3-json-editor demo</div>
    <Vue3JsonEditor
      v-model="state.json"
      :show-btns="true"
      :expandedOnStart="false"
      mode="code"
      lang="zh"
      @json-change="onJsonChange"
      @json-save="onJsonSave"
      @provide-editor="onEditorProvided"
      ref="editorRef"
      @has-error="onError"
    />
    <button type="button" @click="resetJson">reset</button>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
import { Vue3JsonEditor } from "../dist/vue3-json-editor.esm";

export default defineComponent({
  name: "App",
  components: {
    Vue3JsonEditor
  },
  setup() {
    const editorRef = ref();
    const state = reactive({
      json: [{ name: "Dirk", age: 1234 }, { name: "Jason" }]
    });

    function onJsonChange(value) {
      console.log("value:", value);
    }

    function onJsonSave(value) {
      console.log("value:", value);
    }

    function onError(value) {
      console.log("value:", value);
    }

    function resetJson() {
      if (editorRef.value) {
        console.log(editorRef.value.getEditor());
      }
      state.json = [{ name: "Dirk", age: 1234 }, { name: "Jason" }];
    }

    function onEditorProvided(editor: any) {
      console.log(editor);
    }

    return {
      state,
      resetJson,
      onJsonChange,
      onJsonSave,
      onError,
      onEditorProvided,
      editorRef
    };
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
