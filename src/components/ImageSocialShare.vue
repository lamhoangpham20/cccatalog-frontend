<template>
  <section class="sidebar_section social-sharing">
    <social-share-buttons
      :shareURL="shareURL"
      :imageURL="imageURL"
      :shareText="shareText"
      :image="image">
    </social-share-buttons>
  </section>
</template>

<script>
import SocialShareButtons from '@/components/SocialShareButtons';

export default {
  name: 'image-social-share',
  props: ['image'],
  components: {
    SocialShareButtons,
  },
  data: () => ({
    // for SSR, initiates it as an empty value
    shareURL: '',
  }),
  computed: {
    imageURL() {
      return this.image.foreign_landing_url;
    },
    shareText() {
      return encodeURI(`I found an image through CC Search @creativecommons: ${this.imageURL}`);
    },
  },
  mounted() {
    // for SSR, sets the value with window.location, which is only available on client
    this.shareURL = window.location.href;
  },
};
</script>

<style lang="scss" scoped>
  @import '../styles/photodetails.scss';
</style>
