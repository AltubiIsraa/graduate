<script setup>
import { toRef } from "vue";
const props = defineProps(["posts"]);
const Posts = toRef(props, "posts");
</script>
<template>
  {{ Posts }}
</template>
