<template>
  <div class="hello">
      <h1>
        {{current.title}} - {{current.artist}}
      </h1>
      <div class="controls">
        <button class="prev">Prev</button>
        <button class="play" v-if="isPlaying" @click='play'>Play</button>
        <button class="pause" v-else @click='pause'>Pause</button>
        <button class="next" @click='next'>Next</button>
      </div>
      <div class="playlist">
        <button v-for="item in songs" :key="item.src" @click='play(song)' :class="(song.src == current.src) ?  'song play' : 'song'">
          {{item.title}}
        </button>
      </div>
  </div>
</template>

<script>
import { reactive, toRefs } from 'vue'
export default {
  name: 'HelloWorld',
  setup(){
    const state = reactive({
      current: {},
      index: 0,
      isPlaying: true,
      songs: [
        {
          title: 'No Guidance ',
          artist: 'Chris Brown',
          src: require('../assets/Chris Brown - No Guidance (Audio) ft. Drake-192.mp3')
        },
        {
          title: '6LACK ',
          artist: 'Switch',
          src: require('../assets/6LACK - Switch (Official Video)-128.mp3')
        },
        {
          title: 'A Lot ',
          artist: '21 Savage',
          src: require('../assets/21 Savage – A Lot (OG Version)_(Downloadnaija-com).mp3')
        }
      ],
      player: new Audio()
    })

    

    state.current = state.songs[state.index]
    state.player.src = state.current.src


    function pause(){
      state.player.pause()
      state.isPlaying = true
    }
    function play(song){
      if(typeof song.src != "undefined"){
        state.current = song
        state.player.src = state.current.src
      }
      state.player.play()
      state.isPlaying = false
    }

    return{
      ...toRefs(state),
      play,
      pause,
    }
  }
  
}
</script>

<style scoped>
.next{
  cursor: pointer;
}
</style>
