<template>
  <div class="hello">
    {{current.title}}
  </div>
</template>

<script>
import { reactive, toRefs } from 'vue'
export default {
  name: 'HelloWorld',
  setup(){
    const state = reactive({
      current: {
        
      },
      index: 0,
      songs: [
        {
          title: 'Make ',
          artist: 'Omo',
          src: require('../assets/Chris Brown - No Guidance (Audio) ft. Drake-192.mp3')
        },
        songs: [
        {
          title: 'Make ',
          artist: 'Omo',
          src: require('../assets/Chris Brown - No Guidance (Audio) f