<template>
  <div class="app">
    <header>
      <div>
        <h1>
          <img src="./assets/goku.png" alt="goku" class="goku_image" />

          The<strong>Anime</strong>Galaxy
          <img src="./assets/gogeta.png" alt="goku" class="gogeta" />
        </h1>
	</div>
	
	<form class="search-box" @submit.prevent="HandleSearch">
		<input
		type="search"
		class="search-field"
		placeholder="Search for an anime..."
		required
		v-model="search_query"
        />
		<img src="./assets/naruto_baryon.webp" alt="goku" class="naruto_baryon" />
      </form>
    </header>
    <main>
      <div class="cards">
        <AnimeCard
          v-for="anime in animeList"
          :key="anime.mal_id"
          :anime="anime"
        />
      </div>
      <p v-if="animeList.length === 0">Nenhum anime encontrado.</p>
    </main>
  </div>
</template>

<script>
import { ref } from "vue";
import AnimeCard from "./components/AnimeCard";

export default {
  components: {
    AnimeCard,
  },
  setup() {
    const search_query = ref("");
    const animeList = ref([]);
    const loading = ref(false);

    const HandleSearch = async () => {
      loading.value = true;
      try {
        const response = await fetch(
          `https://api.jikan.moe/v4/anime?q=${search_query.value}`
        );
        const data = await response.json();
        animeList.value = data.data || []; // Preenche a lista de animes
        if (animeList.value.length === 0) {
          console.log("Nenhum anime encontrado.");
        }
      } catch (error) {
        console.error("Erro ao buscar animes:", error);
        animeList.value = []; // Limpa a lista em caso de erro
      } finally {
        loading.value = false; // Finaliza o carregamento
      }
    };

    return {
      search_query,
      animeList,
      HandleSearch,
      loading,
    };
  },
};
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Fira Sans", sans-serif;
}

a {
  text-decoration: none;
}

header {
  padding-top: 50px;
  padding-bottom: 50px;
}

header h1 {
  color: #888;
  font-size: 42px;
  font-weight: 400;
  text-align: center;
  text-transform: uppercase;
  margin-bottom: 30px;

  strong {
    color: #313131;
  }

  &:hover {
    color: #313131;
  }
}
.search-box {
  display: flex;
  justify-content: center;
  padding-left: 30px;
  padding-right: 30px;

  .search-field {
    appearance: none;
    background: none;
    border: none;
    outline: none;

    background-color: #f3f3f3;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.15);

    display: block;
    width: 100%;
    max-width: 600px;
    padding: 15px;
    border-radius: 8px;

    color: #313131;
    font-size: 20px;

    transition: 0.4s;

    &::placeholder {
      color: #aaa;
    }

    &:focus,
    &:valid {
      color: #fff;
      background-color: #313131;
      box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.15);
    }
  }
}

main {
  max-width: 1200px;
  margin: 0 auto;
  padding-left: 30px;
  padding-right: 30px;

  .cards {
    display: flex;
    flex-wrap: wrap;
    margin: 0 -8px;
  }
}
body {
  min-height: 100vh; /* Garante que o body ocupe toda a altura da tela */
  background: linear-gradient(
    to bottom,
    #ffc800,
    #fa713f
  ); /* Gradiente de dourado para vermelho */
  background-attachment: fixed; /* Fixar o fundo para não se mover com o conteúdo */
  color: #fff; /* Texto claro */
}

.goku_image {
  width: 45px;
  animation: floatEffect 2.5s ease-in-out infinite;
}

/* Animação para flutuar */
@keyframes floatEffect {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-12px);
  }
  100% {
    transform: translateY(0);
  }
}

.gogeta {
  width: 50px;
  animation: floatEffect 3s ease-in-out infinite;
}

/* Animação para flutuar */
@keyframes floatEffect {
  0% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
  100% {
    transform: translateY(0);
  }
}

.naruto_baryon {
	width: 50px;
	margin-left: 10px;

}

/* Media Queries */
@media (max-width: 768px) {
  header h1 {
    font-size: 32px;
  }

  .search-box {
    padding-left: 20px;
    padding-right: 20px;
  }

  .search-field {
    max-width: 100%;
    font-size: 18px;
  }
}

@media (max-width: 480px) {
  header h1 {
    font-size: 28px;
  }

  .cards {
    justify-content: center;
  }
}
</style>
