<template>
  <VNavigationDrawer
      v-model="show"
      absolute
      temporary
      app
  >
    <VListItem>
      <VListItemAvatar>
        <VImg src="https://randomuser.me/api/portraits/men/78.jpg"></VImg>
      </VListItemAvatar>

      <VListItemContent>
        <VListItemTitle>{{ $root.user.username }}</VListItemTitle>
      </VListItemContent>
    </VListItem>

    <VDivider></VDivider>

    <VList dense>
      <VListItem
          link
          :to="{name: 'app-calendar'}"
      >
        <VListItemIcon>
          <VIcon>{{ icons.CALENDAR }}</VIcon>
        </VListItemIcon>

        <VListItemContent>
          <VListItemTitle>Calendar</VListItemTitle>
        </VListItemContent>
      </VListItem>
      <VListItem
          link
          :to="{name: 'app-shopping-list'}"
      >
        <VListItemIcon>
          <VIcon>mdi-cart-outline</VIcon>
        </VListItemIcon>

        <VListItemContent>
          <VListItemTitle>Einkaufen</VListItemTitle>
        </VListItemContent>
      </VListItem>
    </VList>
  </VNavigationDrawer>
</template>

<script>
import Vue from "vue";
import {iconsMixin} from "@calendar/config/icons";

export default Vue.extend({
  name: "NavigationDrawer",
  mixins: [iconsMixin],
  props: {
    value: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      show: this.value,
    }
  },
  watch: {
    value(show) {
      this.show = show;
    },
    show(show) {
      this.$emit('input', show);
    }
  }
});
</script>

<style scoped>

</style>