<template lang="pug">
  v-container
    license
</template>

<script>
import License from '~/components/License.vue'
export default {
  components: { License },
  head () {
    return {
      title: 'License | N7 World'
    }
  },
  layout: 'light'
}
</script>
