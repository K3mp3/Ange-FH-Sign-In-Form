<script setup lang="ts">
import AdminPageVue from "@/components/adminpage/AdminPage.vue";
import axios from "axios";
import { onMounted, ref } from "vue";

interface IMovie {
  _id: string;
  title: string;
  poster: string;
  link: string;
}

const savedMovie = ref<any>(null);
const movies = ref<IMovie[]>([]);

async function saveMovieInfo(
  moviePoster: File,
  movieImage: File,
  movieTitle: string,
  movieLink: string
) {
  // console.log("poster:", moviePoster, "movieImage:", movieImage, "title:", movieTitle, "movieLink:", movieLink);

  const formData = new FormData();
  formData.append("poster", moviePoster);
  formData.append("image", movieImage);
  formData.append("title", movieTitle);
  formData.append("link", movieLink);

  // console.log("formdata:", formData)

  try {
    const response = await axios.post(
      "http://localhost:3000/movie/savemovie",
      formData
    );
    // console.log("Movie saved successfully!", response.data);

    const { poster, title, link } = response.data;

    // console.log("response", response.data);

    savedMovie.value = {
      poster: poster,
      title: title,
      link: link,
    };

    // console.log("savedMovie.value", savedMovie.value);
  } catch (error) {
    // console.log("Failed to save movie:", error);
  }
}

onMounted(async () => {
  try {
    const response = await axios.get("http://localhost:3000/movie");
    movies.value = response.data;
    console.log(movies.value);
  } catch (error) {
    console.error("Failed to retrieve posters:", error);
  }
});

async function deleteMovie(movie: IMovie) {
  console.log("movie", movie.poster);

  let movieName = movie.poster;
  let movieId = movie._id;

  try {
    const response = await axios.post(
      "http://localhost:3000/movie/deletemovie",
      { movieId: movieId, movieName: movieName }
    );

    const { movie } = response.data;

    console.log("response", response.data);

    location.reload();
  } catch (error) {
    console.log("Failed to save movie:", error);
  }
}
</script>

<template>
  <div>
    <AdminPageVue @movieInfo="saveMovieInfo"></AdminPageVue>

    <div class="large-container">
      <h1>Aktiva filmer</h1>
      <div class="medium-container">
        <div v-for="movie in movies" :key="movie._id" class="movies">
          <img
            :src="`http://localhost:3000/movie/image/${movie.poster}`"
            :alt="movie.title"
          />
          <h3>{{ movie.title }}</h3>
          <button @click="() => deleteMovie(movie)">Radera film</button>
        </div>
      </div>
    </div>
  </div>
</template>
<style scoped>
/* scroll-snap-type: y
  scroll-behavior: smooth */

  .large-container {
    background-color: #f7f7f7;
    padding-top: 40px;
  }

  h1 {
    text-align: center;
  }

  .medium-container {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin: auto;
  }

  .movies {
    display: flex;
    flex-direction: column;
  }

  img {
    max-width: 100%;
    max-height: 300px;
    padding: 20px;
  }

  button {
    width: 100px;
    margin: 10px auto;
  }
</style>
