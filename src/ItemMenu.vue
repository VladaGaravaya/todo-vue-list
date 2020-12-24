<template lang="html">
    <ul class="dropdown-content" :id="'menu'+dataId" :style="active ? activeStyle : '' " @mouseleave="onMouseLeave">
      <li>
        <p v-for="color in colors.slice(1)"
              :class="['color-sm', color]" :id="color"
              @click="onColorChange"></p>
      </li>
    </ul>
</template>

<script>
export default {
  props: ['active', 'colors', 'data-id'],
  template: ``,
  data: function(){
    return {
      activeStyle: {
        width: '26.25px',
        position: 'absolute',
        top: '0',
        right: '3em',
        opacity: 1,
        display: 'block'
      }
    }
  },
  methods: {
    emitColor: function(e){
      this.$emit('new-color', e.target.id)
    },
    onColorChange: function(e){
      this.emitColor(e)
      this.$emit('color-change')
    },
    onMouseLeave: function(){
      this.$emit('mouseleave')
    },
  }
}
</script>
