<template>
  <ul
    :class="['structure__list', {
      'no-offset': level > 4
    }]"
  >
    <li
      :class="['structure__item', {
        'structure__item--opened': showTree || isOpened
      }]"
      @click="showTreeToggle"
    >
      <file-structure-icon
        :type="structure.type"
        class="structure__icon"
      />
      {{ structure.name }}
    </li>
    <template v-if="structure.contents && showTree">
      <FileStructureItem
        v-for="child in structure.contents"
        :key="child.name + level"
        :structure="child"
        :path="currentPath"
        :selected-path="selectedPath"
        :level="level + 1"
        @selected-item="selectedItem($event)"
      />
    </template>
  </ul>
</template>

<script>
import FileStructureIcon from "@/components/Structure/StructureIcon";
export default {
  name: "FileStructureItem",
  components: {FileStructureIcon},
  props: {
    structure: {
      type: [Object],
      default: () => {}
    },
    level: {
      type: Number,
      default: 1
    },
    path: {
      type: String,
      default: ''
    },
    selectedPath: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      showTree: false
    }
  },
  computed: {
    currentPath() {
      return `${this.path}/${this.structure.name}`
    },
    isOpened() {
      return this.currentPath === this.selectedPath
    }
  },
  methods: {
    showTreeToggle() {
      if (this.structure.type === 'directory')
        this.showTree = !this.showTree

      if (this.showTree || this.structure.type !== 'directory')
        this.$emit('selected-item', {
          type: this.structure.type,
          path: this.currentPath
        })
    },
    selectedItem(event) {
      this.$emit('selected-item', event)
    }
  }
}
</script>

<style scoped>
  .no-offset {
    padding: 0;
  }
</style>
