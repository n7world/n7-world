<template lang="pug">
  v-navigation-drawer(fixed clipped app v-model="isActive")
    v-text-field(
      append-icon="search"
      label="Search"
      single-line
      hide-details
      solo
      v-model="search"
      v-on:keyup.enter="submit"
      clearable
    ).ma-2
    v-list(dense)
      template(v-for="item in items")
        v-list-group(v-if="item.items" v-bind:prepend-icon="item.icon" no-action)
          v-list-item(slot="activator" ripple)
            v-list-item-content
              v-list-item-title {{ item.title }}
          template(v-for="(subItem, i) in item.items")
            v-divider(v-if="item.divider")
            v-list-item(v-else :key="i" v-bind="{to: subItem.href, href: subItem.href }" ripple nuxt)
              v-list-item-content
                v-list-item-title {{ subItem.title }}
        v-subheader(v-else-if="item.header") {{ item.header }}
        v-divider(v-else-if="item.divider")
        v-list-item(v-else v-bind="{ to: item.href, href: item.href }" ripple rel="noopener" nuxt)
          v-list-item-action(v-if="item.icon")
            v-icon {{ item.icon }}
          v-list-item-content
            v-list-item-title {{ item.title }}
          v-list-item-avatar(v-if="item.icon === 'book'" color="primary" size="20").white--text {{ bookmarkCount }}
</template>

<script>
import { mapActions, mapGetters } from 'vuex'

export default {
  data () {
    return {
      items: [
        {
          header: 'Player\'s Manual'
        },
        {
          title: 'Introduction',
          icon: 'code',
          href: '/'
        },
        {
          title: 'Rules',
          icon: 'gavel',
          items: [
            { title: 'Step-by-step Characters', icon: 'supervised_user_circle', href: '/phb/rules/character-creation' },
            { title: 'Beyond 1st Level', icon: 'tending_up', href: '/phb/rules/beyond-first-level' },
            { title: 'Using Ability Scores', icon: 'gamepad', href: '/phb/rules/using-ability-scores' },
            { title: 'Missions', icon: 'map', href: '/phb/rules/missions' },
            { title: 'Equipment', icon: 'category', href: '/phb/rules/equipment' },
            { title: 'Finances', icon: 'money', href: '/phb/rules/finances' },
            { title: 'Vehicles', icon: '', href: '/phb/rules/vehicles' },
            { title: 'Combat', icon: '', href: '/phb/rules/combat' },
            { title: 'Spellcasting', icon: '', href: '/phb/rules/spellcasting' },
            { title: 'Monsters', icon: '', href: '/phb/rules/monsters' }
          ]
        },
        {
          title: 'Characters',
          icon: 'face',
          items: [
            { href: '/phb/classes', title: 'Classes' },
            { href: '/phb/races', title: 'Races' },
            { href: '/phb/feats', title: 'Feats' },
            { href: '/phb/backgrounds', title: 'Backgrounds' }
          ]
        },
        {
          title: 'Equipment',
          icon: 'build',
          items: [
            { href: '/phb/weapons', title: 'Weapons' },
            { href: '/phb/weapon-mods', title: 'Weapon Mods' },
            { href: '/phb/armor/mods', title: 'Armor Mods' },
            { href: '/phb/armor/sets', title: 'Armor Sets' },
            { href: '/phb/programs', title: 'Omni-tool Programs' },
            { href: '/phb/grenades', title: 'Grenades' },
            { href: '/phb/tools-kits', title: 'Tools & Kits' },
            { href: '/phb/vehicles', title: 'Vehicles' }
          ]
        },
        {
          title: 'Spells & Powers',
          icon: 'whatshot',
          href: '/phb/spells'
        },
        {
          title: 'Bestiary',
          icon: 'pets',
          href: '/phb/bestiary'
        },
        {
          title: 'Appendix',
          icon: 'vertical_split',
          items: [
            { href: '/phb/appendix/conditions', title: 'Conditions' },
            { href: '/phb/appendix/skills', title: 'Skills' },
            { href: '/phb/appendix/weapon-properties', title: 'Weapon Properties' }
          ]
        },
        {
          title: 'Bookmarks',
          icon: 'book',
          href: '/phb/bookmarks'
        },
        {
          title: 'divider',
          divider: true
        },
        {
          header: 'Tools'
        },
        {
          title: 'For GMs',
          icon: 'extension',
          items: [
            { href: '/for-gms/loot-generator', title: 'Loot Generator' },
            { href: '/for-gms/grunts', title: 'Grunt Generator' },
            { href: '/for-gms/armor-creation', title: 'Creating Armor' },
            { href: '/for-gms/encounter-builder', title: 'Encounter Builder' },
            { href: '/missions', title: 'Missions' }
          ]
        },
        {
          title: 'divider',
          divider: true
        },
        {
          header: 'N7 World'
        },
        { title: 'Tabletop Assets', href: '/assets' },
        { title: 'About the Project', href: '/about' },
        { title: 'Changelog', href: '/changelog' },
        { title: 'Offline / PDF version', href: '/print/pdf' },
        { title: 'License', href: '/license' }
      ]
    }
  },
  computed: {
    ...mapGetters(['bookmarkCount', 'getVersion', 'phbSearch']),
    isActive: {
      get () {
        return this.$store.state.sidebar
      },
      set (val) {
        this.$store.commit('toggleSidebar', val)
      }
    },
    search: {
      get () {
        return this.phbSearch
      },
      set (val) {
        this.setPhbSearch(val)
      }
    }

  },
  methods: {
    ...mapActions(['setPhbSearch']),
    submit () {
      this.$router.push({
        path: '/phb/search'
      })
      if (this.$vuetify.breakpoint.mdAndDown) {
        this.isActive = false
      }
    }
  }
}
</script>
