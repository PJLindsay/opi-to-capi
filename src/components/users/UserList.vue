<template>
  <base-container>
    <h2>Active Users</h2>
    <base-search
      @search="updateSearch"
      :search-term="enteredSearchTerm"
    ></base-search>
    <div>
      <button @click="sort('asc')" :class="{ selected: sorting === 'asc' }">
        Sort Ascending
      </button>
      <button @click="sort('desc')" :class="{ selected: sorting === 'desc' }">
        Sort Descending
      </button>
    </div>
    <ul>
      <user-item
        v-for="user in displayedUsers"
        :key="user.id"
        :user-name="user.fullName"
        :id="user.id"
        @list-projects="$emit('list-projects', $event)"
      ></user-item>
    </ul>
  </base-container>
</template>

<script>
import { computed, ref } from 'vue';
import UserItem from './UserItem.vue';
import useSearch from '../../hooks/search.js';

export default {
  components: {
    UserItem
  },
  props: ['users'],
  emits: ['list-projects'],
  setup(props) {

    /*  ----------------------  SEARCH LOGIC ---------------------- */
    /*  ---------------  moved to /hooks/search.js ---------------- */
    const { enteredSearchTerm, availableItems, updateSearch } = useSearch(
      props.users,
      'fullName'
    );

    /*  ----------------------  SORT LOGIC ---------------------- */
    const sorting = ref(null);
    const displayedUsers = computed(function() {
      if (!sorting.value) {
        return availableItems.value;
      }
      return availableItems.value.slice().sort((u1, u2) => {
        if (sorting.value === 'asc' && u1.fullName > u2.fullName) {
          return 1;
        } else if (sorting.value === 'asc') {
          return -1;
        } else if (sorting.value === 'desc' && u1.fullName > u2.fullName) {
          return -1;
        } else {
          return 1;
        }
      });
    });

    function sort(mode) {
      sorting.value = mode;
    }

    /*  ----------------------  Expose methods/computed/variables to template ---------------------- */
    return {
      displayedUsers,
      enteredSearchTerm,
      sorting,
      sort,
      updateSearch
    };
  },
  watch: {
    enteredSearchTerm(val) {
      setTimeout(() => {
        if (val === this.enteredSearchTerm) {
          this.activeSearchTerm = val;
        }
      }, 300);
    }
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
