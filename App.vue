<template>
  <div>
<look></look>
<copy></copy>
  </div>
</template>

<script>
import copy from './components/copy.vue';
import look from './components/look.vue'

export default {
  name: 'App',
  components: {
    look,
    copy,

  }
}
</script>

<style lang="css">
*{
  margin: 0;
  padding: 0;
  font-family: 'Poppins',sans-serif;
  box-sizing: border-box;
}

body{
  background: #222;
}
.card{
  width:70%;
  max-width: 470px;
  background: linear-gradient(135deg,#00feba,#5b548a);
  color: #fff;
  margin:100px auto 0;
  border-radius: 20px;
  padding: 40px 35px;
  text-align: center;
}
</style>
