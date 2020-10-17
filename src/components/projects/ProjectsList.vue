<template>
  <base-container v-if="user">
    <h2>{{ user.fullName }}: Projects</h2>
    <base-search v-if="hasProjects" @search="updateSearch" :search-term="enteredSearchTerm"></base-search>
    <ul v-if="hasProjects">
      <project-item v-for="prj in availableProjects" :key="prj.id" :title="prj.title"></project-item>
    </ul>
    <h3 v-else>No projects found.</h3>
  </base-container>
  <base-container v-else>
    <h3>No user selected.</h3>
  </base-container>
</template>

<script>
import { computed, watch, toRefs } from 'vue'
import ProjectItem from './ProjectItem.vue'
import useSearch from '../../hooks/search.js'

export default {
  components: {
    ProjectItem,
  },
  props: ['user'],
  setup(props) {

    // to watch one prop (if you have many props in a component)
    // otherwise watch(props, function() ...) would fire every time *any* prop changes
    const { user } = toRefs(props)

    // props are reactive, but prop values are not
    // so lets use a computed property
    const projects = computed(function() {
      return user.value ? user.value.projects : []
    })

    const { enteredSearchTerm, availableItems, updateSearch } = useSearch(
      projects,
      'title'
    );

    const hasProjects = computed(function() {
      return user.value.projects && availableItems.value.length > 0
    })

    watch(user, function() {
      updateSearch('')
    })

    return {
      availableProjects: availableItems,
      enteredSearchTerm,
      hasProjects,
      updateSearch
    }
  }
}
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>