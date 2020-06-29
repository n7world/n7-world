<template lang="pug">
  v-container
    div.my-10.text-center
      p.display-4 N7 World
      p.display-1.
        A Mass Effect TTRPG Homebrew
      p.title v{{ version }}
    div(v-for="(rule, index) in rules" v-bind:key="index")
      rule-card(:id="rule.id")
</template>

<script>
import { mapGetters } from 'vuex'
import RuleCard from '~/components/RuleCard.vue'
import rules from '~/static/data/rules'

export default {
  components: { RuleCard },
  computed: {
    ...mapGetters('phb', {
      version: 'version',
      pages: 'pages'
    }),
    rules () {
      return rules.filter(rule => rule.section === this.pages[this.$route.name].rules)
    }
  },
  head () {
    return {
      title: 'Player\'s Manual | N7 World'
    }
  },
  layout: 'phb'
}
</script>

<style lang="scss">
  #phbLogo {
    width: 100%;
    height: auto;
  }

  @media screen and (min-width: 960px) {
    #phbLogo {
      width: auto;
      height: 90px;
    }
  }
</style>
