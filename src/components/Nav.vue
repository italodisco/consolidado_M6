<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
    <div class="container">
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ml-auto">
          <li>
            <router-link class="nav-link" to="/">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/admin">Tu Cuenta</router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'nav-comp',
};
</script>

<style scoped>
.nav{
  color: blue;
}
.navbar-brand {
  font-weight: bold;
  color: #705151;

}

.nav-link {
  color: #705151;
  margin-right: 10px;
}

.nav-link:hover {
  color: #ccc;
}
</style>
