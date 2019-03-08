<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  sockets: {
    connect () {
      console.log('Now you are connected with socket.io')
    },
  },
}
</script>
