<template>
  <div>
    <div class="header">
      <div class="contenedor">
        <img src="/img/ico-logo.png" style="width: 3.5em; min-width: 3.5em;">
      </div>
      <div class="contenedor">
        <span class="text-white font-weight-bold">{{ texto1 }}</span>
      </div>
    </div>
    <Nuxt />
  </div>
</template>
<script>
export default {
  data() {
    return {
      texto1:'Frontend Test',
    }
  },
}
</script>
<style>
body{
  background: -webkit-linear-gradient(top, rgba(0,250,104,1) 0%, rgba(0,247,255,1) 100%);
  background-repeat: no-repeat;
  background-attachment: fixed
}
.header{
  display: flex;
  flex-direction: column;
  justify-content: center;
  margin: 1em;
}
.contenedor{
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  padding: 0.2em;
  /*border: 4px solid #000;*/
}
</style>
