<script setup>
import { toRef } from "vue";
const props = defineProps(["user"]);
const User = toRef(props, "user");
</script>
<template>
  <div class="card">
    <h3>User Details</h3>
    <p>UserName is :</p>
    <h5>{{ User.username }}</h5>
    <p>Email is :</p>
    <h5>{{ User.email }}</h5>
  </div>
</template>

<style>
.card {
  box-shadow: 0 4px 8px 0 rgba(255, 255, 255, 0.827);
  transition: 0.3s;
  width: 100%;
  border-radius: 5px;
}

.card:hover {
  box-shadow: 0 8px 16px 0 rgb(255, 255, 255);
}

.container {
  padding: 2px 16px;
}
</style>
