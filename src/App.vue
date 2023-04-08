<script setup>
import { watchEffect } from 'vue'
import { Repl, ReplStore } from '@vue/repl'
import '@vue/repl/style.css'

const store = new ReplStore({
  serializedState: location.hash.slice(1),
  showOutput: true,
  outputMode: 'preview',
})

watchEffect(() => history.replaceState({}, '', store.serialize()))

store.setImportMap({
  imports: {
    "vue": "./vue.runtime.esm-browser.js",
    "simple-mind-map": "./simpleMindMap.esm.js"
  }
})
</script>

<template>
  <div class="replContainer">
    <Repl style="height: 100%" :store="store" :ssr="false" :showCompileOutput="false" />
  </div>
</template>

<style scoped>
.replContainer {
  position: absolute;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
}
</style>
