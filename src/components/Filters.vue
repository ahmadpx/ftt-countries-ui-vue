<template>
  <FiltersContainer>
    <h2>Filters</h2>

    <FilterGroup
      title="languages"
      :filter-data="filters.languages"
      :is-selected-filter="isSelectedFilter"
      :toggle-filter="toggleFilter"
      :filters-state="filtersState"
    />

    <FilterGroup
      title="currencies"
      :filter-data="filters.currencies"
      :is-selected-filter="isSelectedFilter"
      :toggle-filter="toggleFilter"
      :filters-state="filtersState"
    />

    <FilterGroup
      title="regions"
      :filter-data="filters.regions"
      :is-selected-filter="isSelectedFilter"
      :toggle-filter="toggleFilter"
      :filters-state="filtersState"
    />
    <ResetBtn @click="resetAllFilters()">reset all filters</ResetBtn>
  </FiltersContainer>
</template>

<script>
import { autorun, toJS } from "mobx";
import FilterGroup from "./FilterGroup";
import { FiltersContainer, ResetBtn } from "./Filters.styles";
export default {
  name: "Filters",
  components: {
    FilterGroup,
    ResetBtn,
    FiltersContainer
  },
  props: {
    store: Object
  },
  data() {
    return {
      filters: {},
      filtersState: {}
    };
  },
  methods: {
    toggleFilter(filter) {
      return this.store.countriesList.toggleFilter(filter);
    },
    isSelectedFilter(filter) {
      return this.store.countriesList.isSelectedFilter(filter);
    },
    resetAllFilters() {
      return this.store.countriesList.resetAllFilters();
    }
  },
  mounted() {
    autorun(() => {
      this.filters = this.store.countriesList.countriesStore.filters;
      this.filtersState = toJS(this.store.countriesList.filtersState);
    });
  }
};
</script>

<style scoped></style>
