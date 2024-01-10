<script setup>
import SearchIcon from "../assets/icons/icon-search.svg";
const emit = defineEmits(["filterChanged"]);

const onFilter = (e) => {
  console.log("filtered");
  console.log(e.target.value);
  emit("filterChanged", e.target.value);
};
</script>

<template>
  <div class="nav">
    <div class="nav-logo">
      <span class="brand-color">Code</span>
      <span>lândia</span>
    </div>
    <div class="nav-search">
      <div class="input-group">
        <img :src="SearchIcon" alt="search icon" class="input-icon" />
        <input @change="onFilter" placeholder="Pesquisar no blog" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.nav {
  background-color: #17171a;
  padding: 64px 0;
  height: 290px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 40px;
  color: #ffffff;
}

.nav-logo {
  font-family: "Space Grotesk", sans-serif !important;
  font-weight: 500;
  font-size: 40px;
}

.brand-color {
  color: #e07b67;
}

.nav-search {
  width: 60%;
}
</style>