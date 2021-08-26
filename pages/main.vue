<template>
  <div class="w-full min-h-screen">
    <Navigation />
    <PlayerTable />
  </div>
</template>
<script>
import Navigation from '../components/Navigation.vue'
import PlayerTable from '../components/PlayerTable.vue'
export default {
  components: { Navigation, PlayerTable },
}
</script>
