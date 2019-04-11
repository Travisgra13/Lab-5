<template>
  <div class="home">
  <image-gallery :photos="photos" />
  <a href="https://github.com/Travisgra13/Lab-5.git">Link</a>
</div>
</template>

// @ is an alias to /src
<script>
// @ is an alias to /src
import ImageGallery from '@/components/ImageGallery.vue'

export default {
  name: 'home',
  components: {
    ImageGallery
  },
  computed: {
    photos() {
      return this.$store.state.photos;
    }
  },
  async created() {
    await this.$store.dispatch("getAllPhotos");
  },
}
</script>
