<template>
  <div class="w-full flex flex-row justify-start">
    <side-bar />
    <MainView />
  </div>
</template>

<script>
import Sidebar from '../components/SideBar.vue'
import MainView from './main.vue'
export default {
  components: { MainView, Sidebar },
}
</script>
