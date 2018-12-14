<template>
  <div class="container">
    <Transition
      name="fade"
      enter-active-class="animated fadeIn"
      leave-active-class="animated fadeOut"
    >
      <img
        v-show="loaded"
        :src="img_url"
        class="image center"
        @load="isLoaded"
      >
    </Transition>
    <div v-show="!loaded">
      <img
        class="center"
        src="../assets/loading.gif"
      >
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      img_url: '',
      loaded: false
    }
  },
  created () {
    this.fetch()
  },
  methods: {
    fetch () {
      setInterval(function () {
        this.$http.get(this.$store.state.Slice.api_url)
          .then(({ data }) => {
            this.img_url = data.url
          })
      }.bind(this), 3000)
    },
    isLoaded () {
      this.loaded = true
    }
  }
}
</script>

<style lang="scss">
@import url('https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.css');

.container {
  width: 100%;
  height: 100%;
}

.center {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.image {
  animation-duration: 0.25s;
  height: 100vh;
}
</style>
