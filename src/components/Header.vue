<template>
  <div class="header">
    <h1>{{ title }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Header',
  props: {
    title: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .header {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 75px;
    background: #2c3e50;
  }
  h1 {
    margin: 0;
  }
</style>
