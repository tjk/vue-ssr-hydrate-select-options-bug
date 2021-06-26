<template>
  <div style="margin-bottom:20px">Toggle the select below, notice emitted type is string. Then click button to force update, the change select value and notice emitted type is boolean.</div>

  <div v-if="shown" style="margin-bottom:20px">
    <select v-model="model">
      <option :value="true">true</option>
      <option :value="false">false</option>
    </select>
  </div>

  <button @click="forceUpdate" style="margin-bottom:20px" :disabled="!lines.length">force update</button>

  <div>
    <div v-for="(line, idx) in lines" :key="idx">{{line}}</div>
  </div>
</template>

<script setup>
import { ref, watch, nextTick } from "vue"
const model = ref(true)
const shown = ref(true)
const forceUpdate = async () => {
  shown.value = false
  await nextTick()
  shown.value = true
  lines.value.push("forced update!")
}
const lines = ref([])
watch(model, v => {
  lines.value.push(`emitted value=${v} type=${typeof v}`)
})
</script>
