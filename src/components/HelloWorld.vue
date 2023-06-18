<script setup lang="ts">
import { ref, onMounted } from 'vue'
import { getName, getTauriVersion, getVersion, hide, show } from '@tauri-apps/api/app';


defineProps<{ msg: string }>()

const count = ref(0)
const appname = ref("")
const appTauriVersion= ref("")
const appVersion = ref("")
onMounted(async () => {
  const res = await getName()
  appname.value = res
 
  const ver = await getTauriVersion()
  appTauriVersion.value = ver
  
  const appver = await getVersion()
  appVersion.value = appver
})

async function onHide(){
  console.log("hide clicked")
  await hide();
}
async function onShow(){
  console.log("show clicked")
  await show();
}
</script>

<template>
  <h1>{{ msg }}- {{ appname }} - {{  appTauriVersion }}</h1>
  <h1>- {{  appVersion }}</h1>
  <button @click="onHide">Hide</button>
  <button @click="onShow">Show</button>

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
