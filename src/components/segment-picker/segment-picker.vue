<template>
  <div class="cube-segment-picker">
    <cube-sub-picker
      v-for="(item, index) in data"
      :key="index"
      ref="pickers"
      :is="item.cascade ? 'cube-cascade-picker' : 'cube-picker'"
      :data="item.data"
      :index="index"
      @select="select()">
    </cube-sub-picker>
  </div>
</template>

<script>
import CubeSubPicker from './sub-picker.vue'

const COMPONENT_NAME = 'cube-segment-picker'
const EVENT_SUB_SELECT = 'sub-select'
const EVENT_SELECT = 'select'

export default {
  name: COMPONENT_NAME,
  components: {
    CubeSubPicker
  },
  props: {
    data: {
      type: Array,
      default() {
        return []
      }
    },
    cascade: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      
    }
  },
  methods: {
    show() {
      this.$refs.pickers[0].show()
    },
    select(selectedVal, selectedIndex, selectedText) {
      this.$emit(EVENT_SUB_SELECT, index, selectedVal, selectedIndex, selectedText)
      if (index < this.data.length - 1) {
        this.$refs.pickers[index + 1].show()
      } else {
        this.$emit(EVENT_SELECT)
      }
    },
    select() {
      debugger
    }
  }
}
</script>
