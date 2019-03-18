<template>
  <div class="c-home">
    <h1>NBA PLAYERS</h1>
    <Team :playersList="players"/>
  </div> 
</template>

<script>
// @ is an alias to /src
import Team from '../components/Team.vue'
import players from '../assets/json/players.json'

export default {
  name: 'home',
  data () {
    return {
      players: players,
    }
  },
  components: {
    Team
  }
}
</script>
