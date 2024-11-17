<template>
  <div class="relative w-64" @focusout="handleFocusOut" tabindex="0">
    <input
      type="text"
      v-model="searchQuery"
      @focus="showDropdown = true"
      @keydown.down.prevent="highlightNext()"
      @keydown.up.prevent="highlightPrevious()"
      @keydown.enter.prevent="selectHighlighted()"
      placeholder="Виберіть елемент..."
      class="w-full p-2 border rounded-lg focus:outline-none focus:ring"
    />
    <button v-if="selectedItems.length > 0" @click="clearSelection" class="absolute right-2 top-2 text-gray-500">&times;</button>
    <div v-if="showDropdown" class="absolute z-10 w-full mt-1 bg-white border rounded-lg shadow-lg">
      <ul>
        <li v-for="(item, index) in filteredItems" :key="index" @click="toggleItemSelection(item)"
            :class="['p-2 cursor-pointer', highlightedIndex === index ? 'bg-blue-100' : '', isSelected(item) ? 'bg-blue-200' : '']"
            @mouseenter="highlightedIndex = index"
        >
          <span v-if="item.icon" class="mr-2">{{ item.icon }}</span>{{ item.label }}
        </li>
        <li v-if="filteredItems.length === 0" class="p-2 text-gray-500">Нічого не знайдено</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SearchableDropdown',
  props: {
    items: {
      type: Array,
      required: true
    },
    multiple: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      searchQuery: '',
      showDropdown: false,
      highlightedIndex: -1,
      selectedItems: []
    };
  },
  computed: {
    filteredItems() {
      return this.items.filter(item => item.label.toLowerCase().includes(this.searchQuery.toLowerCase()));
    }
  },
  methods: {
    toggleItemSelection(item) {
      if (this.multiple) {
        const index = this.selectedItems.findIndex(selectedItem => selectedItem.label === item.label);
        if (index === -1) {
          this.selectedItems.push(item);
        } else {
          this.selectedItems.splice(index, 1);
        }
        this.$emit('select', this.selectedItems);
      } else {
        this.selectedItems = [item];
        this.searchQuery = item.label;
        this.showDropdown = false;
        this.$emit('select', item);
      }
    },
    isSelected(item) {
      return this.selectedItems.some(selectedItem => selectedItem.label === item.label);
    },
    highlightNext() {
      if (this.highlightedIndex < this.filteredItems.length - 1) {
        this.highlightedIndex++;
      }
    },
    highlightPrevious() {
      if (this.highlightedIndex > 0) {
        this.highlightedIndex--;
      }
    },
    selectHighlighted() {
      if (this.highlightedIndex >= 0 && this.highlightedIndex < this.filteredItems.length) {
        this.toggleItemSelection(this.filteredItems[this.highlightedIndex]);
      }
    },
    clearSelection() {
      this.selectedItems = [];
      this.searchQuery = '';
      this.$emit('select', null);
    },
    handleFocusOut(event) {
      // Перевіряємо, чи фокус перейшов на елемент, який не є частиною компонента
      if (!this.$el.contains(event.relatedTarget)) {
        this.showDropdown = false;
      }
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
