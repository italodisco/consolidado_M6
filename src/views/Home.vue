<template>
  <div class="container">
    <h1 class="text-center m-3">Lista de Juegos Disponibles</h1>
    <div class="row">
      <div class="col-12 col-md-4" v-for="(game, index) in games" :key="index">
        <div class="box">
          <div class="card">
            <div class="card-image">
              <img :src="game.background_image" class="card-img-top" alt="">
            </div>
            <div class="card-body">
              <h5 class="card-title">{{ game.name.toUpperCase() }}</h5>
              <ul class="list-group">
                <li class="list-group-item"><b>Rating:</b> {{ game.rating }} ⭐️</li>
                <li class="list-group-item"><b>Lanzamiento:</b> <br> <small><i class="bi bi-calendar3"></i></small> {{ game.released }}</li>
                <li class="list-group-item"><b>Actualización:</b> <br><small><i class="bi bi-calendar-plus"></i></small> {{ game.updated }}</li>
              </ul>
              <div class="card-footer">
                <i class="bi bi-pencil-square mx-1 click" @click="toReviews(game.name)">Opinar</i> |
                <i class="bi bi-chat-square-heart mx-1 click" @click="toAdmin(game.name)"></i>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "home-comp",
  data() {
    return {
      games: [],
    };
  },
  methods: {
    getData() {
      let apiKey = 'key=de294bb09054413cb1d75970171acf08';
      axios.get(`https://api.rawg.io/api/games?${apiKey}`)
        .then(response => {
          let { results } = response.data;
          this.games = results.map(game => ({
            ...game,
            released: this.dateReleased(game.released),
            updated: this.dateUpdated(game.updated),
          }));
        })
        .catch(error => {
          console.error(error);
        });
    },
    toReviews(name) {
      this.$router.push(`/opiniones/${name}`);
    },
    toAdmin(name) {
      this.$router.push(`/admin/${name}`);
    },
    dateUpdated(date) {
      return new Date(date).toLocaleString('es-CL');
    },
    dateReleased(date) {
      return new Date(date).toLocaleDateString('es-CL');
    },
  },
  created() {
    this.getData();
  },
};
</script>

<style scoped>
.box {
  background-color: #f8f9fa;
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 20px;
}

.card {
  border: none;
  border-radius: 5px;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
}

.card-image {
  height: 200px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.card-image img {
  max-height: 100%;
  max-width: 100%;
}

.card-body {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  text-align: center;
}

.card-title {
  text-transform: uppercase;
  font-size: 1.2rem;
}

.bi-calendar3,
.bi-calendar-plus {
  color: steelblue;
}

.click:hover {
  cursor: pointer;
  text-shadow: 0 0 .1rem gray;
}

a {
  text-decoration: none;
  color: #000;
}
</style>
