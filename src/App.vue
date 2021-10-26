<template>
  <div id="app">
    <structure-item
        :structure="structure"
        :selected-path="path"
        @selected-item="selectedItem($event)"
        class="structure"
    />
    <div class="details" v-if="type && path">
      Is opened <strong>{{ type }}</strong> {{ path }}
    </div>
  </div>
</template>

<script>
import structure from '../public/static/node_modules.json'
import StructureItem from "@/components/Structure/StructureItem";

export default {
  name: 'App',
  components: {
    StructureItem
  },
  data() {
    return {
      structure,
      type: '',
      path: ''
    }
  },
  methods: {
    selectedItem(obj) {
      this.type = obj.type
      this.path = obj.path
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box
}

body, ul[class], li {
  margin: 0
}

ul[class], ol[class] {
  list-style: none
}

#app {
  display: flex;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.structure {
  width: 35%;
}

.structure__list {
  padding-left: 15px;
}

.structure__item {
  display: flex;
  align-items: center;
  border-radius: 5px;
  margin: 4px 0;
  padding: 8px 8px;
  cursor: pointer;
  transition: .3s;
}

.structure__item:hover {
  background: #f7f3f7
}

.structure__item--opened {
  background-color: #eee;
}

.structure__item--opened:hover {
  background-color: #ccc;
}

.structure__icon {
  margin-right: 10px;
}

.details {
  padding: 15px;
}
</style>
