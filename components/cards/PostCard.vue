<template lang="pug">
  v-card(hover v-bind:to="post.url" nuxt).post__card
    v-img(:src="post.image" v-bind:height="height")
    v-card-text
      div.overline {{ post.date | formatDate('YYYY-MM-DD') }}
      p.headline.mb-0 {{ post.title }}
      p {{ post.description }}

</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      default: () => { return {} }
    },
    height: {
      type: String,
      default: ''
    }
  }
}
</script>

<style lang="scss">
  .post__card {
    .card__media__content {
      background: rgba(0, 0, 0, 0.2);
      -webkit-transition: background 150ms ease-out;
      -moz-transition: background 150ms ease-out;
      -o-transition: background 150ms ease-out;
      transition: background 150ms ease-out;
    }

    &:hover {
      .card__media__content {
        background: rgba(0, 0, 0, 0);
      }
    }
  }
</style>
