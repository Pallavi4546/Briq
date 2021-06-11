<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <strong style="font-size:50px">Briq Assignment</strong>
    <User />
  </div>
</template>

<script>
// @ is an alias to /src
import User from '@/components/User.vue'

export default {
  name: 'Home',
  components: {
    User
  }
}
</script>
