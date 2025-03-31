<template>
  <div class="header container">
    <h1 @click="navigateTo('/')">{{ topHeader.logoTitle }}</h1>
    <div>
      <ul>
        <li v-for="(item, index) in topHeader.leftLinks" :key="index">
          <NavSubItem
            v-if="item"
            :name="item.title"
            :url="item.url"
          ></NavSubItem>
        </li>
      </ul>
    </div>
  </div>
</template>

<script lang="ts" setup>
import type { TopHeader } from "../types";

const props = defineProps({
  topHeader: { type: Object as PropType<TopHeader>, required: true },
});
</script>
