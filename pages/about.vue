<template lang="pug">
  v-container.text-center
    h1.display-4 About N7 World
    v-row(justify="center").mt-10
      v-col(cols="12" sm="8")
        p.
          N7 World is a community-developed tabletop RPG based on the popular video game Mass Effect. It utilizes
          many rules from the Dungeons and Dragons 5th Edition system, but has introduced a variety of new mechanics
          and content.
    v-row(justify="center").mt-5
      v-col(cols="12" sm="8").my-2
        div.text-xs-center
          h2.headline Image Attributuions
          p.px-5.
            Any images not listed were either created by the community or are sourced from #[a(href="http://masseffect.wikia.com/wiki/Mass_Effect_Wiki" target="_blank")  Mass Effect Wiki].
    v-row
      v-col(v-for="att in attributions" v-bind:key="att.attribution" cols="12" sm="6" md="4" lg="3")
        v-card(:href="att.source" v-bind:alt="att.title" target="_blank" hover)
          v-img(:src="att.path" height="150px" contain)
          v-card-text
            span {{ att.attribution }}
</template>

<script>
import AboutCard from '~/components/cards/AboutCard.vue'
import attributions from '~/static/data/attributions'

export default {
  components: { AboutCard },
  data () {
    return {
      attributions
    }
  },
  head () {
    return {
      title: 'About | N7 World'
    }
  },
  layout: 'dark'
}
</script>
