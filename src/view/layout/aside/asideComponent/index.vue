<template>
  <component :is="menuComponent" :routerInfo="routerInfo" v-if="!routerInfo.hidden">
    <template v-if="routerInfo.children && routerInfo.children.length">
      <AsideComponent
        :key="item.name"
        :routerInfo="item"
        v-for="item in routerInfo.children"
      />
    </template>
  </component>
</template>

<script>
import MenuItem from './menuItem'
import AsyncSubmenu from './asyncSubmenu'
import { computed } from 'vue'

export default {
  name: 'AsideComponent',
  props: {
    routerInfo: {
      default: function () {
        return null
      },
      type: Object
    }
  },
  components: {
    MenuItem,
    AsyncSubmenu
  },
  setup (props) {
    const menuComponent = computed(() => {
      if (
        props.routerInfo.children &&
        props.routerInfo.children.filter((item) => !item.hidden).length
      ) {
        return 'AsyncSubmenu'
      } else {
        return 'MenuItem'
      }
    })

    return { menuComponent }
  }
}
</script>
<style lang="scss"></style>
