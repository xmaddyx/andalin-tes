<template>
  <v-app>
	<div>
      <div>
        <a href="#/">Home</a> |
        <a href="#/register">Register</a>
      </div>
	</div>
	<component :is="currentView" />
  </v-app>
</template>

<script>
import Home from './components/Home';
import Register from './components/Register';
import NotFound from './components/NotFound'

const routes = {
	'/': Home,
	'/register': Register
}

export default {
  data() {
    return {
      currentPath: window.location.hash
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
      this.currentPath = window.location.hash
    })
  }
}
</script>
