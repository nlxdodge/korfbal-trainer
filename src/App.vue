<template>
  <div
    class="nav-hamburger"
    @click="navVisible = true"
  >
    <font-awesome-icon :icon="['fas', 'bars']" />
  </div>
  <Sidebar
    v-model:visible="navVisible"
    :show-close-icon="false"
  >
    <nav>
      <p>Korfbal Trainer</p>
      <router-link
        to="/"
        @click="navVisible = false"
      >
        <font-awesome-icon :icon="['fas', 'running']" />
        Maak Training
      </router-link>
      <router-link
        to="/exercises"
        @click="navVisible = false"
      >
        <font-awesome-icon :icon="['fas', 'list']" />
        Oefeningen
      </router-link>
      <router-link
        to="/info"
        @click="navVisible = false"
      >
        <font-awesome-icon :icon="['fas', 'question-circle']" />
        Info
      </router-link>
      <a
        href="#"
        @click="navVisible = false"
      >
        <font-awesome-icon :icon="['fas', 'arrow-alt-circle-left']" />
        Sluiten
      </a>
    </nav>
  </Sidebar>
  <router-view />
</template>

<script lang="ts">
import Sidebar from 'primevue/sidebar'
import { defineComponent } from 'vue'

export default defineComponent({
  components: {
    Sidebar
  },
  data () {
    return {
      navVisible: false
    }
  },
  beforeMount () {
    this.$store.dispatch('loadData')
    console.log(
      'Loaded data from json file, categories:',
      this.$store.state.categories.length,
      'exercises:',
      this.$store.state.exercises.length
    )
  }
})
</script>

<style lang="scss">
$primary-color: #cc0c0c;

html {
  background-color: $primary-color;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.nav-hamburger {
  color: #fff;
  position: fixed;
  top: 20px;
  left: 20px;
  font-size: 2.25rem;
  -webkit-filter: drop-shadow(0 0 0.1rem  rgba(0, 0, 0, 0.5));
  filter: drop-shadow(0 0 0.1rem  rgba(0, 0, 0, 0.5));
}

nav {
  display: flex;
  flex-direction: column;

  p {
    text-align: center;
    color: $primary-color;
    font-weight: bold;
    font-size: 1.25rem;
    margin: 10px 0;
  }

  a {
    text-decoration-line: none;
    color: $primary-color;
    font-size: 1.25rem;
    padding: 10px;
    border-bottom: 2px solid $primary-color;

    svg {
      width: 75px;
    }
  }
}
</style>
