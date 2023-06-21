<script setup lang="ts">
import { ref } from 'vue'
import { readText, writeText } from '@tauri-apps/api/clipboard';


defineProps<{ msg: string }>()

const count = ref(0)
const clipboardText = ref("")

async function copy() {
  // read from the clipboard
  console.log("hhhhhhhhh --- in")
  const text = await readText().catch((error) => { console.log(error) });
  if (text !== null) {
    console.log(text)
    clipboardText.value = text
    console.log("hhhhhhhhh - paste")
  }
  console.log("hhhhhhhhh -- out")
}
async function paste() {
  // write to the clipboard
  console.log("hhhhhhhhh", clipboardText.value)
  await writeText(clipboardText.value + ' => Tauri is awesome!').catch((error) => {
    console.log("efforr")
    console.log(error)
  })

}
</script>

<template>
  <h1>{{ msg }}</h1>
  <button @click="copy">Get the content from the clipboard</button>
  <button @click="paste">Change the content of the clipboard</button>
  <br />
  <textarea size="60" style="font-size:2rem">{{ clipboardText }}</textarea>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank">create-vue</a>, the official Vue + Vite
    starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>