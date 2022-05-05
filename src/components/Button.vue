<template>
  <button @click="onClick()" :style="{background: color}" class="btn">{{ text }}</button>
<!--  v-on:click="onClick()" oder einfach @click-->
</template>

<script>
export default {
  name: 'Button',
  props: {
    text: String,
    color: String
  },
  methods:{
    onClick(){
    this.$emit('toggle-add-task')
    }
  }
}
</script>