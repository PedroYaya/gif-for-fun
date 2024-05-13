<template>
  <div class="gif-list">
    <ul>
      <li v-for="(item, index) in gifs" :key="`gif-${index}`" @click="$emit('set-current-gif', item)">
        <div class="text-data">
          <div>
            <span> <strong>Username:</strong> {{ item.username }}</span>
          </div>
          <div>
            <span> <strong>Type:</strong>: {{ item.type }}</span>
            <span> <strong>Rating:</strong>: {{ item.rating }}</span>
          </div>
        </div>
        <img :src="getImageSrc(item)"/>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'GifList',
  props: {
    gifs: Array
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

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 10px;
  border: 1px solid #fafafa;
  padding: 10px;
  border-radius: 7px;
  cursor: pointer;
}

img {
  width: 30px;
  height: 30px;
  border-radius: 6px;
}

.text-data {
  display: grid;
  grid-template-columns: 70% 30%;
  text-align: left;
  width: 100%;
}

.text-data span {
  display: block;
}


@media screen and (max-width: 768px) {
  .text-data {
    grid-template-columns: 50% 50%;
  }
}

</style>