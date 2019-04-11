<template>
<div>
  <div class="image" v-for="photo in photos" v-bind:key="photo._id">
    <img :src="photo.path" v-on:click="redirect(photo._id)"/>
    <p class="photoTitle">{{photo.title}}</p>
    <p class="photoDate">
  <span v-if="photo.user.name">{{photo.user.name}}, </span>
  {{formatDate(photo.created)}}
</p>
    <p>{{photo.description}}</p>
  </div>
</div>
</template>

<script>
import moment from 'moment';

export default {
  name: 'ImageGallery',
  props: {
    photos: Array
  },
   methods: {
    formatDate(date) {
      if (moment(date).diff(Date.now(), 'days') < 15)
        return moment(date).fromNow();
      else
        return moment(date).format('d MMMM YYYY');
    },
    redirect(id) {
      console.log("in direct thingie and id is " + id);
      this.$store.commit('setPhotoId', id);
      this.$router.push('/PhotoPage');
    }
  }
}
</script>

<style scoped>
.photoTitle {
  margin: 0px;
  font-size: 1.2em;
}

.photoDate {
  margin: 0px;
  font-size: 0.9em;
  font-weight: normal;
}

p {
  margin: 0px;
}

.image {
  margin: 0 0 1.5em;
  display: inline-block;
  width: 100%;
}

.image img {
  max-width: 600px;
  max-height: 600px;
  image-orientation: from-image;
}
</style>
