<template>
  <div class="d-flex">
    <Search
      :modelValue="routeQuery"
      @update:modelValue="input => $emit('update:modelValue', input)"
      :placeholder="$t('searchPlaceholder')"
      class="flex-auto pr-2"
    />
    <div class="border-left" style="height: 44px">
      <UiDropdown
        top="3.5rem"
        right="1.0rem"
        class="text-left"
        style="z-index: 1"
        @select="redirectSearch"
        :items="searchOptions"
      >
        <span v-text="searchSelectedOption" class="ml-3" />
        <Icon name="arrow-down" class="ml-1 mr-2 pr-1" />
      </UiDropdown>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    redirectSearch(e) {
      this.$router.push({
        name: e,
        query: this.routeQuery ? { q: this.routeQuery } : {}
      });
    }
  },
  computed: {
    searchSelectedOption() {
      return (
        this.searchOptions.find(option => option.action === this.$route.name)
          ?.text || 'home'
      );
    },
    searchOptions() {
      return [
        {
          text: this.$t('spaces'),
          action: 'home'
        },
        {
          text: this.$t('networks'),
          action: 'networks'
        },
        {
          text: this.$t('strategiesPage'),
          action: 'strategies'
        },
        {
          text: this.$t('plugins'),
          action: 'plugins'
        },
        {
          text: this.$t('skins'),
          action: 'skins'
        }
      ];
    },
    routeQuery() {
      return this.$route.query.q;
    }
  }
};
</script>
