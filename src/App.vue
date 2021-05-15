<template>
  <div
    class="drop-zone"
    @drop="onDrop($event, 1)"
    @dragenter.prevent
    @dragover.prevent
  >
    <div
      v-for="item in getList(1)"
      :key="item.id"
      class="drag-el text"
      draggable="true"
      @dragstart="startDrag($event, item)"
    >
      {{ item.title }}
    </div>
  </div>

  <div
    class="drop-zone"
    @drop="onDrop($event, 2)"
    @dragenter.prevent
    @dragover.prevent
  >
    <div
      v-for="item in getList(2)"
      :key="item.id"
      class="drag-el text"
      draggable="true"
      @dragstart="startDrag($event, item)"
    >
      {{ item.title }}
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const items = ref([
  {
    id: 0,
    title: "Item A",
    list: 1,
  },
  {
    id: 1,
    title: "Item B",
    list: 1,
  },
  {
    id: 2,
    title: "Item C",
    list: 2,
  },
]);

const getList = (list: any) => items.value.filter((item) => item.list === list);

const startDrag = (evt: any, item: any) => {
  evt.dataTransfer.dropEffect = "move";
  evt.dataTransfer.effectAllowed = "move";
  evt.dataTransfer.setData("itemID", item.id);
};

const onDrop = (evt: any, list: any) => {
  const itemID = evt.dataTransfer.getData("itemID");
  const item = items.value.find((item) => item.id == itemID);
  if (item) {
    item.list = list;
  }
};

const color = "red";
</script>

<style scoped>
.drop-zone {
  background-color: #eee;
  margin-bottom: 10px;
  padding: 10px;
}

.drag-el {
  background-color: #fff;
  margin-bottom: 10px;
  padding: 5px;
}

.text {
  color: v-bind(color);
}
</style>