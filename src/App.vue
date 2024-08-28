<script setup>
import {reactive,ref} from "vue";
import leftBlockJson from './assets/json/left-block.json';
import rightBlockJson from './assets/json/right-block.json';

let selectedLeftItems = reactive([]);
let selectedRightItem = ref({});
let finalLeftItem = ref({});

const selectLeftItem = (item) => {
  const foundItem = selectedLeftItems.find(i => i.id === item.id);

  if (!foundItem) {
    selectedLeftItems.push(item);
  }
};

const selectRightItem = (item) => {
  selectedRightItem.value = item;
};

const selectFinalLeftItem = (item) => {
  finalLeftItem.value = item;
};
</script>

<template>
  <main>
    <div class="container">
      <div class="left-part">
        <div class="left-part__top">
          <div class="selected-left-part-item" v-for="item in selectedLeftItems" :key="item.id" @click="selectFinalLeftItem(item)">
            {{ item.name }}
          </div>
          <div class="final-left-part-item" v-if="finalLeftItem.id">
            Selected: {{ finalLeftItem.name }}
          </div>
        </div>
        <div class="left-part__bottom">
          <div class="left-part-item" v-for="item in leftBlockJson" :key="item.id" @click="selectLeftItem(item)">
            {{ item.name }}
          </div>
        </div>
      </div>

      <div class="right-part">
        <div class="right-part__top">
          <div class="selected-left-part-item">
            {{ selectedRightItem.name }}
          </div>
        </div>
        <div class="right-part__bottom">
          <div class="right-part-item" v-for="item in rightBlockJson" :key="item.id" @click="selectRightItem(item)">
            {{ item.name }}
          </div>
        </div>
      </div>
    </div>
  </main>
</template>
