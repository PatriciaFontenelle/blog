<script setup>
import heartIcon from "../assets/icons/icon-heart.svg";
import activeHeartIcon from "../assets/icons/icon-heart-active.svg";
import { ref, onMounted } from "vue";

const props = defineProps(["item"]);

const active = ref(false);

const currentCard = ref(null);

const isOverflow = ref(false);

const handleLike = () => {
  console.log("currentCard");
  console.log(currentCard.value);
  console.log("Clicou");
  console.log(props.item);
  props.item.liked = !props.item.liked;
};

const checkOverflow = () => {
  const el = currentCard.value;
  if (!el) return;
  return el.scrollHeight != Math.max(el.offsetHeight, el.clientHeight);
};

onMounted(() => {
  isOverflow.value = checkOverflow();
})
</script>

<template>
  <div class="card" :class="[{ active }]">
    <div class="card-header">
      <div class="card-date">{{ item?.date }}</div>
      <button class="icon-btn" @click="handleLike()">
        <img
          alt="like button"
          :src="item?.liked ? activeHeartIcon : heartIcon"
        />
      </button>
    </div>
    <div class="card-title">
      {{ item?.title }}
    </div>
    <div ref="currentCard" class="card-description">
      {{ item?.description }}
    </div>
    <button v-if="isOverflow" @click="active = !active" class="show-more-btn">
      {{ active ? "Mostrar menos" : "Mostrar mais" }}
    </button>
  </div>
</template>

<style>
.card {
  background-color: #252529;
  width: 100%;
  padding: 40px;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  gap: 15px;
  max-height: 250px;
  position: relative;
  transition: 5s ease-in-out;
}

.card.active {
  height: auto;
  max-height: 1000px;
  transition: 5s ease;
}

.card:hover {
  /* border: 2px solid #e07b67; */
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.card-date,
.card-like {
  color: #e07b67;
  font-weight: 500;
}

.card-title {
  font-size: 1.5em;
  font-weight: 500;
}

.card-description {
  color: #afabb6;
  font-size: 1.25em;
  max-height: 100%;
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  transition: 5s ease;
}

.card.active > .card-description {
  display: block;
}

.show-more-btn {
  position: absolute;
  right: 0;
  left: 0;
  bottom: 0;
  padding: 16px;
  background-color: #e07b67;
  border-radius: 0 0 8px 8px;
  display: none;
  cursor: pointer;
}

.card:hover > .show-more-btn {
  display: block;
}
</style>