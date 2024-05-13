
<template>
  <div>
    <input type="text" v-model="term" @keydown="onKeyDown($event)" />
    <button @click="$emit('on-search', term)">SEARCH</button>
  </div>
</template>

<script>
export default {
  name: 'GifSearch',
  data() {
    return {
      term: '',
    }
  },
  methods: {
    onKeyDown(ev) {
      if (ev.keyCode === 13) this.$emit('on-search', this.term);
    }
  }
}
</script>
