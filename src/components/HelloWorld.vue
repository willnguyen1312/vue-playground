<template>
  <div>
    <div
      class="drop-zone"
      @drop="onDrop($event, 1)"
      @dragover.prevent
      @dragenter.prevent
    >
      <div
        class="drag-el"
        v-for="item in listOne"
        :key="item.title"
        draggable
        @dragstart="startDrag($event, item)"
      >
        {{ item.title }}
      </div>
    </div>
    <div
      class="drop-zone"
      @drop="onDrop($event, 2)"
      @dragover.prevent
      @dragenter.prevent
    >
      <div
        class="drag-el"
        v-for="item in listTwo"
        :key="item.title"
        draggable
        @dragstart="startDrag($event, item)"
      >
        {{ item.title }}
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, computed } from "vue";

export default defineComponent({
  name: "HelloWorld",
  setup: () => {
    const dndData = reactive([
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

    const listOne = computed(() => dndData.filter((item) => item.list === 1));

    const listTwo = computed(() => dndData.filter((item) => item.list === 2));

    const startDrag = (evt: any, item: any) => {
      console.log(123);
      evt.dataTransfer.dropEffect = "move";
      evt.dataTransfer.effectAllowed = "move";
      evt.dataTransfer.setData("itemID", item.id);
    };

    const onDrop = (evt: any, list: any) => {
      const itemID = evt.dataTransfer.getData("itemID");
      const item = dndData.find((item) => item.id == itemID);
      if (item) {
        item.list = list;
      }
    };

    return { listOne, listTwo, startDrag, onDrop };
  },
});
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
</style>
