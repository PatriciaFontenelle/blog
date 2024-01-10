
<script setup>
import Layout from "./components/Layout.vue";
import Post from "./components/Post.vue";
import { ref, onMounted } from "vue";

const searchStr = ref("");

const filteredPosts = ref([]);

const posts = ref([
  {
    id: 1,
    date: "17 de ago, 2024",
    title: "O que é linguagem de programação? Conheça as principais",
    description:
      "Uma das mais populares vertentes da tecnologia da informação, a área de programação segue tendo muita demanda de trabalho justamente pela velocidade com que dispositivos tecnológicos vêm avançando. Uma das mais populares vertentes da tecnologia da informação, a área de programação segue tendo muita demanda de trabalho justamente pela velocidade com que dispositivos tecnológicos vêm avançando. Uma das mais populares vertentes da tecnologia da informação, a área de programação segue tendo muita demanda de trabalho justamente pela velocidade com que dispositivos tecnológicos vêm avançando. Uma das mais populares vertentes da tecnologia da informação, a área de programação segue tendo muita demanda de trabalho justamente pela velocidade com que dispositivos tecnológicos vêm avançando. Uma das mais populares vertentes da tecnologia da informação, a área de programação segue tendo muita demanda de trabalho justamente pela velocidade com que dispositivos tecnológicos vêm avançando.",
    liked: true,
  },
  {
    id: 2,
    date: "12 de jul, 2024",
    title: "GitHub agora permite fazer login sem precisar de senha",
    description:
      "O GitHub anunciou nesta quarta-feira (12) o acesso a partir das passkeys, método de autenticação sem senhas. A novidade está disponível em uma versão beta pública e pode substituir a autenticação em dois fatores.",
    liked: false,
  },
  {
    id: 3,
    date: "21 de jun, 2024",
    title: "Por que os hiperlinks são azuis em sua maioria?",
    description:
      "Quem navega na internet, certamente já percebeu que ela conta com diversos recursos para tornar a nossa vida mais fácil. Entre essas opções podemos mencionar os hiperlinks – uma palavra ou termo clicável que direciona o leitor.",
    liked: false,
  },
]);

const filterChanged = (e) => {
  const filteredData = posts.value.filter(
    (p) =>
      p.date.includes(e) || p.title.includes(e) || p.description.includes(e)
  );

  filteredPosts.value = filteredData;
};

onMounted(() => {
  filteredPosts.value = posts.value;
});
</script>

<template>
  <div class="app-container">
    <Layout @filterChanged="filterChanged" />
    <span>{{ searchStr }}</span>
    <div class="posts-container">
      <Post v-for="post in filteredPosts" :key="post?.id" :item="post" />
    </div>
  </div>
</template> 

<style>
.app-container {
  width: 100vw;
  min-height: 100vh;
  background-color: #121214;
}
.posts-container {
  max-width: 60%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 80px 0;
  margin: 0 auto;
  gap: 40px;
}
</style>
