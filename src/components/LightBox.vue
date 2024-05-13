<template>
  <div class="card">
    <button @click="$emit('close')">X</button>
    <img :src="getImageSrc(gif)"/>    
  </div>
</template>

<script>
export default {
  name: 'LightBox',
  props: {
    gif: Object
  },
  methods: {
    getImageSrc(item) {
      const data = item.images['downsized'];
      if (data) return data.url;
      return '';
    }
  }
}
</script>

<style scoped>

.card {
  max-width: 400px;
  max-height: 400px;
  overflow: hidden;
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  top: 20%;
  background: #e3e3e3;
}

img {
  max-width: 100%;
}

button {
  position: absolute;
  right: 10px;
  top: 10px;
}

</style>