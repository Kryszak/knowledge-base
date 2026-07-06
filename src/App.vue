<template>
  <div class="layout">
    <!-- MENU -->
    <aside class="menu">
      <ul>
        <li
          v-for="doc in docs"
          :key="doc.path"
          :class="{ active: doc.path === selected }"
          @click="selected = doc.path"
        >
          {{ doc.title }}
        </li>
      </ul>
    </aside>

    <!-- CONTENT -->
    <main class="content">
      <MdFile
        v-if="selected"
        :key="selected"
        :file="selected"
      />
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import MdFile from "./components/MdFile.vue";

const docs = ref([]);
const selected = ref(null);

onMounted(async () => {
  const res = await fetch("/knowledge-base/index.json");
  docs.value = await res.json();

  selected.value = docs.value[0]?.path ?? null;
});
</script>

<style scoped lang="scss">
.layout {
  display: flex;
  height: 100vh;
}

.menu {
  width: 240px;
  border-right: 1px solid #ddd;
  padding: 10px;
}

.menu ul {
  list-style: none;
  padding: 0;
}

.menu li {
  padding: 8px;
  cursor: pointer;
}

.menu li.active {
  font-weight: bold;
  background: #646b79;
}

.content {
  flex: 1;
  padding: 16px;
  overflow: auto;
}
</style>
