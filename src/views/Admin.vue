<template>
  <div>
    <div class="userIn text-center mt-5" v-show="!user">
      <h1>Ingresa tus datos para acceder a la información
      </h1>
      <button class="btn btn-outline-dark" @click="datoPrompt">Ingresar Datos</button>
    </div>
    <div class="userInfo" v-show="user">
      <div class="userInfo__name bg-dark text-white px-3 text-center">
        <i class="bi bi-person-circle"></i>
        <h1 class="mb-2">¡Te damos la bienvenida!</h1>
        <h4 class="text-center">{{ fullName }}</h4>
      </div>
      <div class="userInfo__resumen flex-fill px-3">
        <h1>Resumen de tu cuenta</h1>
        <p>Diste like al juego <span class="fw-bold">{{ game }}</span></p>
        <div class="card">
          <div class="card-body text-center">
            <h5 class="card-title">¿Comprar coins para el juego?</h5>
            <button class="btn btn-warning" @click="addCoins"><i class="bi bi-currency-exchange"></i> ++</button>
          </div>
          <div class="card-footer text-end">
            <p v-if="coins === 50" class="text-center">Has alcanzado el máximo de Coins</p>
            <div class="progress" role="progressbar" aria-label="coins" :aria-valuenow="coins*2" aria-valuemin="0" aria-valuemax="100">
              <div class="progress-bar progress-bar-striped text-dark" :style="{ width: (coins * 2) + '%', backgroundColor: color }"><b>{{ coins * 2 }}%</b></div>
            </div>
            {{ coins }} Coins Compradas
          </div>
        </div>
        <h4 class="text-center mt-3">Resumen de {{ game }}</h4>
        <div class="row row-cols-3 row-cols-md-3 g-2 my-3 text-center">
          <div class="col">
            <div class="card h-100 text-success">
              <div class="card-header">% Finalización</div>
              <div class="card-body">
                <p class="card-text fw-bold">
                  <i class="bi bi-star" v-show="finaliz >= 0 && finaliz < 33"> {{ finaliz }}</i>
                  <i class="bi bi-star-half" v-show="finaliz > 33 && finaliz < 66"> {{ finaliz }}</i>
                  <i class="bi bi-star-fill" v-show="finaliz > 66"> {{ finaliz }}</i>
                </p>
              </div>
            </div>
          </div>
          <div class="col">
            <div class="card h-100 text-primary">
              <div class="card-header text-center">Logros</div>
              <div class="card-body">
                <p class="card-text fw-bold">
                  <i class="bi bi-trophy"> {{ logros }}</i>
                </p>
              </div>
            </div>
          </div>
          <div class="col">
            <div class="card h-100 text-info">
              <div class="card-header text-center">Recompensas</div>
              <div class="card-body">
                <p class="card-text fw-bold">
                  <i class="bi bi-award"> {{ recomp }}</i>
                </p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'admin-comp',
  props: ['game'],
  data() {
    return {
      nombre: '',
      apellido: '',
      user: false,
      coins: 0,
      color: '',
      finaliz: 0,
      recomp: 0,
      logros: 0,
      re: /^(?=.{1,40}$)[A-zÀ-ú]+(?:[-'\s][A-zÀ-ú]+)*$/,
    };
  },
  computed: {
    fullName() {
      return `${this.nombre} ${this.apellido}`;
    },
  },
  methods: {
    datoPrompt() {
      this.nombre = prompt('Ingresa tu nombre');
      this.apellido = prompt('Ingresa tu apellido');
      if (this.re.test(this.nombre) && this.re.test(this.apellido)) this.user = true;
    },
    randomNum() {
      return Math.round(Math.random() * 10);
    },
    backgroundChange() {
      if (this.coins <= 20) {
        this.color = 'green';
      } else {
        this.coins > 20 && this.coins < 31 ? (this.color = 'gold') : (this.color = 'red');
      }
    },
    addCoins() {
      if (this.coins < 50) {
        this.coins++;
        this.backgroundChange();
      }
    },
  },
  created() {
    this.coins = this.randomNum() * 5;
    this.finaliz = this.randomNum() * 10;
    this.logros = this.randomNum() * 10;
    this.recomp = this.randomNum() * this.randomNum();
    this.backgroundChange();
  },
};
</script>

<style>
.userInfo {
  display: flex;
  justify-content: space-between;
}

.userInfo__name {
  height: 93vh;
}

.bi-person-circle {
  font-size: 5rem;
}

.card-text {
  margin: 0 !important;
}
</style>
