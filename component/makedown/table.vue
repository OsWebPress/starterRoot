<template>
  <div class="overflow-x-auto my-4">
    <table class="w-full border-collapse text-sm text-stone-700">
      <thead>
        <tr>
          <th
            v-for="(header, i) in headers"
            :key="i"
            class="bg-amber-100 border border-amber-300 px-4 py-2 text-left font-semibold"
          >
            <LoadComponent _component="makedown/richText" :body="header" />
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(row, ri) in rows" :key="ri">
          <td
            v-for="(cell, ci) in row"
            :key="ci"
            class="bg-amber-50 border border-amber-300 px-4 py-2"
          >
            <LoadComponent _component="makedown/richText" :body="cell" />
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  body: { type: String, default: '' }
})

const isSeparator = (line) => /^\|[\s|:-]+\|?\s*$/.test(line.trim())

const parseRow = (line) =>
  line.split('|').slice(1, -1).map(cell => cell.trim())

const tableData = computed(() => {
  const lines = props.body.split('\n').filter(l => l.trim().startsWith('|'))
  if (lines.length < 2) return { headers: [], rows: [] }
  const headers = parseRow(lines[0])
  const rows = lines.slice(1).filter(l => !isSeparator(l)).map(parseRow)
  return { headers, rows }
})

const headers = computed(() => tableData.value.headers)
const rows = computed(() => tableData.value.rows)
</script>
