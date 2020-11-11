<template>
  <div class="body">
    <Clock />
  </div>
</template>

<script>
import Clock from './components/Clock.vue';

export default {
  name: 'App',
  components: {
    Clock,
  },
};
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
}

.body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #091921;
}
</style>
