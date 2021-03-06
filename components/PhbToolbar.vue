<template lang="pug">
  v-app-bar(dark fixed app
    clipped-left
    v-bind:clippedRight="typeof page.rules !== 'undefined'"
    v-bind:tabs="classPage"
  )
    v-app-bar-nav-icon(v-on:click="toggleSidebar").hidden-lg-and-up
    // Race mobile display
    v-menu(:nudge-width="100" v-if="$vuetify.breakpoint.smAndDown && toolbarMenuItems")
      v-toolbar-title(slot="activator")
        span {{ pageName }}
        v-icon arrow_drop_down
      v-list
        v-list-tile(v-for="item in toolbarMenuItems" v-bind:key="item" v-bind="{to: { name: $route.name, params: { id: item }}}")
          v-list-tile-title {{ item | fidtt }}
    // All other mobile displays
    v-toolbar-title(v-else)
      nuxt-link(to="/").nav-brand.hidden-sm-and-down
        v-img(src="/icon.png" width="36")
    v-btn(text)
      span.hidden.sm-and-down N7 World
      span.hidden-md-and-up {{ pageName }}

    v-spacer

    // Additional Toolbar items
    v-toolbar-items.hidden-sm-and-down
      v-btn(v-for="(item, index) in primaryNavigation" v-bind:key="index" v-bind:to="item.route" text)
        span {{ item.title }}
      v-btn(href="https://discord.gg/c2UnqkH" target="_blank" text)
        v-avatar(size="32" tile)
          img(src="/images/misc/Discord-Logo-Color.svg" alt="Discord Logo")

    // Tabs
    v-tabs(v-if="classPage && $vuetify.breakpoint.smAndDown" slot="extension" v-model="classTab" color="grey darken-4"
            slider-color="white" id="mobileTabs" grow show-arrows).hidden-md-and-up
      v-tab(v-for="tab in classTabs" v-bind:key="tab.id" v-bind:href="`#${tab.id}`" ripple) {{ tab.name }}

    span.hidden-md-and-up
      v-btn(icon @click="setSearchbar(true)" v-if="page.list") #[v-icon search]
      v-btn(icon @click="toggleMobileFilterDialog" v-if="page.list")  #[v-icon filter_list]
      v-btn(icon dark @click="toggleRulebar" v-if="page.rules") #[v-icon view_list]
</template>

<script>
import { createNamespacedHelpers } from 'vuex'
const { mapActions, mapGetters } = createNamespacedHelpers('phb')

export default {
  computed: {
    ...mapGetters(['pages', 'primaryNavigation', 'races', 'classes', 'activeClassTab', 'classTabs', 'searchbar']),
    classTab: {
      get () {
        return this.activeClassTab
      },
      set (value) {
        this.updateActiveClassTab(value)
      }
    },
    page () {
      return this.pages[this.$route.name] ? this.pages[this.$route.name] : {}
    },
    pageName () {
      if (this.pages[this.$route.name]) {
        return this.$route.params.id
          ? `${this.page.name} - ${this.$options.filters.capitalize(this.$route.params.id)}`
          : this.page.name
      } else {
        return ''
      }
    },
    classPage () {
      return this.$route.name === 'phb-classes-id'
    },
    racePage () {
      return this.$route.name === 'phb-races-id'
    },
    toolbarMenuItems () {
      if (this.classPage) {
        return this.classes
      }
      if (this.racePage) {
        return this.races
      }
      return false
    }
  },
  methods: {
    ...mapActions(['toggleSidebar', 'updateActiveClassTab', 'toggleRulebar', 'toggleMobileFilterDialog', 'setSearchbar'])
  }
}
</script>
