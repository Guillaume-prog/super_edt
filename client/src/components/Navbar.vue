<template>
  <header>
    <div>
      <!-- Insert logo -->
      <h1>SUPER<span>EDT</span></h1>
    </div>
    
  </header>
</template>

<style scoped>
  header {
    width: 100%;
    padding: 20px;
    margin-bottom: 20px;
    background: #efefef;
  }

  header h1 {
    font-size: 1.8em;
    font-weight: 200;
    letter-spacing: 0.1em;
  }

  header h1 span {
    font-weight: 800;
  }
</style>

<script>
  export default {
    name: 'Navbar',

    data: () => ({
      
    })
  }
</script>
