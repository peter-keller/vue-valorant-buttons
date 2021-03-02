<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'ServeDev',
});
</script>

<template>
  <div id="app">
    <div class="buttons">
      <VButton type="a" color="secondary" :outline="true" href="#" />
      <VButton type="a" color="secondary" :outline="false" href="#"/>
      <VButton type="a" color="primary" :outline="true" href="#" />
      <VButton type="a" color="primary" :outline="false" href="#" />

      <VButton type="button" color="secondary" :outline="true"  />
      <VButton type="button" color="secondary" :outline="false" />
      <VButton type="button" color="primary" :outline="true" />
      <VButton type="button" color="primary" :outline="false" />
    </div>
  </div>
</template>

<style lang="scss" scoped>
#app {
  background-color: #0f1923;
}

.buttons {
  padding: 100px 0;
  margin: 0 auto;
  width: 500px;
}
</style>