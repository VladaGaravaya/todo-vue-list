<template lang="html">
  <li style="position:relative;">
    <div :class="['collapsible-header', this.data.color + '-bd']">
      <span :class="['material-icons', 'check', this.data.color + '-txt']"
            @click="onCheck">
        {{ data.checked
          ? 'check_box'
          : 'check_box_outline_blank' }}
      </span>
      <p class="limit">
        <span :class="['h-txt', this.data.color + '-txt']" @click="onTextClick">
          {{ data.text }}
        </span>
      </p>
      <span class="material-icons right head-info dropdown-button"
            :data-activates="menuId" @click="toggleActive">
        more_vert
      </span>
      <span class="material-icons right rose-txt head-info"
            @click="onRemove">
        delete
      </span>
      <span @click="onStarChange"
            class="material-icons right sun-txt head-info">
          {{ data.starred
            ? 'grade'
            : 'star_border' }}
      </span>
      <item-menu :data-id="data.id" :active="active" :colors="colors"
                            @mouseleave="onMouseLeave"
                            @new-color="onNewColor" @color-change="onColorChange">
      </item-menu>
    </div>
  </li>
</template>

<script>
import ItemMenu from './ItemMenu.vue'

export default {
  props: ['colors', 'data'],
  components: { ItemMenu },
  data: function(){
    return {
      active: false,
      isViewOpen: false,
      menuId: 'menu' + this.data.id
    }
  },
  methods: {
    onCheck: function(){
      this.$emit('check')
    },
    onColorChange: function(){
      this.$emit('color-change')
    },
    onMouseLeave: function(){
      this.active = false
    },
    onNewColor: function(color){
      this.$emit('new-color', color)
    },
    onStarChange: function(){
      this.$emit('star-change')
    },
    onRemove: function(){
      this.$emit('remove')
    },
    toggleActive: function(){
      this.active = !this.active
    },
    onTextClick: function(){
      this.isViewOpen = true
    }
  }
}
</script>
