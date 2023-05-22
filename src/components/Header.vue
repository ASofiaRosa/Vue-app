<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container-fluid">
      <router-link to="/" class="navbar-brand">Stock trader</router-link>
      <div class="collapse navbar-collapse">
        <ul class="nav navbar-nav me-auto mb-2 mb-lg-0">
          <router-link
            to="/portfolio"
            class="nav-link"
            active-class="active"
            tag="li"
            >Portfolio</router-link
          >
          <router-link
            to="/stocks"
            class="nav-link"
            active-class="active"
            tag="li"
            >Stocks</router-link
          >
        </ul>

        <ul class="nav navbar-nav navbar-right">
          <li><a href="#" class="nav-link">End Day</a></li>
          <li class="nav-item dropdown">
            <a
              class="nav-link dropdown-toggle"
              href="#"
              role="button"
              data-bs-toggle="dropdown"
              aria-expanded="false"
            >
              Save & Load
            </a>
            <ul class="dropdown-menu">
              <li><a class="dropdown-item" href="#">Save Data</a></li>
              <li><a class="dropdown-item" href="#">Load Data</a></li>
            </ul>
          </li>
        </ul>
        <strong class="navbar-text navbar-right">Funds: {{ funds }}</strong>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  computed: {
    funds() {
      return this.$store.getters.funds
    },
  },
}
</script>
