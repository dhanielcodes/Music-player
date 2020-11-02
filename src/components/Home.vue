<template>
  <div class="hello">
    <div class="playlist" :class="{open: open}">
      <img class="top" :class="{open: open}" @click="open = !open" src="../assets/top.svg" alt="" srcset="">
      <h1>PLAYLIST</h1>
      <div class="songsList">
          <button class="songl" v-for="song in songs" :key="song.src" @click='play(song)' :class="(song.src == current.src) ? 'song playing' : 'song'">
            <h2>{{song.title}}</h2> <br>
            {{song.artist}}
          </button>
      </div>
        
    </div>

     <div class='sang'>
       <img class="logo" src="../assets/logo.svg" alt="" srcset="">
          <div class="name">
            <h1>
              {{current.title}}
            </h1> 
            {{current.artist}}
          </div>
          <div class="controls">
            <button class="prev" @click='prev'><img src="../assets/prev.svg" alt="" srcset=""></button>
            <button class="play" v-if="isPlaying" @click='play'><img src="../assets/play.svg" alt="" srcset=""></button>
            <button class="pause" v-else @click='pause'><img src="../assets/pause.svg" alt="" srcset=""></button>
            <button class="next" @click='next'><img src="../assets/next.svg" alt="" srcset=""></button>
          </div>
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
      open: false,
      isPlaying: true,
      songs: [
        {
          title: 'No Guidance ',
          artist: 'Chris Brown',
          src: require('../assets/Chris Brown - No Guidance (Audio) ft. Drake-192.mp3')
        },
        {
          title: 'SWITCH ',
          artist: '6LACK',
          src: require('../assets/6LACK - Switch (Official Video)-128.mp3')
        },
        {
          title: 'A LOT - ft Jcole ',
          artist: '21 Savage',
          src: require('../assets/21 Savage – A Lot (OG Version)_(Downloadnaija-com).mp3')
        },
        {
          title: 'UNDECIDED ',
          artist: 'Chris Brown',
          src: require('../assets/Chris_Brown_-_Undecided_Mp3bullet.ng.mp3')
        },
        {
          title: 'HOTLINE BLING',
          artist: 'Drake',
          src: require('../assets/Drake - Hotline Bling-128.mp3')
        },
        {
          title: 'RANSOM',
          artist: 'Lil Tecca',
          src: require('../assets/Lil_Tecca_-_Ransom_talkglitz.tv.mp3')
        },
        {
          title: 'MIDDLE CHILD',
          artist: '21 Savage',
          src: require('../assets/J_Cole_-_Middle_Child_talkglitz.tv.mp3')
        },
        {
          title: 'THUNDERCLOUDS',
          artist: 'LSD',
          src: require('../assets/LSD - Thunderclouds (Official Video) ft. Sia, Diplo, Labrinth-128.mp3')
        },
        {
          title: '101 FM',
          artist: 'Little Simz',
          src: require('../assets/Little Simz - 101 FM (Official Video)-64.mp3')
        },
        {
          title: 'BLACKJACK fr Cordea',
          artist: 'Blackjack',
          src: require('../assets/01 BLACKJACK (feat. YBN Cordae) Rem.mp3')
        },
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

    function next(){
      state.index++
      if(state.index > state.songs.length - 1){
        state.index = 0
      }

      state.current = state.songs[state.index]
      play(state.current)
    }

    function prev(){
      state.index--
      if(state.index < 0){
        state.index = state.songs.length - 1
      }

      state.current = state.songs[state.index]
      play(state.current)
    }

    return{
      ...toRefs(state),
      play,
      pause,
      next,
      prev
    }
  }
  
}
</script>

<style scoped>
.hello{
    display: grid;
  grid-template-columns: 30% 70%;
  grid-gap: 20px;
}
button{
  cursor: pointer;
  outline: none;
   background: none;
  border: none;
}
.playlist{
  background: black;
  border-radius: 10px 10px 0px 0px;
  height: 95vh;
  overflow: hidden;
  overflow-Y: scroll;
}
.playlist::-webkit-scrollbar{
  width: 7px;
  padding: 10px;
}
.playlist::-webkit-scrollbar-thumb{
  background: #FFE600;
  border-radius:0px 200px 200px 200px;
}
.top{
  display: none;
}
.songsList{
  display: flex;
  justify-content: space-around;
  flex-direction: column;
  width: 100%;
}
.songl h2{
  font-weight: 300;
}
.songl, .playlist h1{
  padding: 20px;
  background: none;
  color: white;
  border: none;
  border-bottom: 1px solid grey;
  text-align: left;
  font-weight: 300;
}
.sang{
  color: white;
  text-align: center; 
}
.logo{
  width: 100%;
  height: 70vh;
}
.controls{
  display: flex;
  justify-content: space-around;
  margin-top: 30px;
}
.name h1{
  font-weight: 400;
}
@media (max-width: 1060px){
  .hello{
     grid-template-columns: 100%;
  grid-gap: 20px;
  }
  .playlist{
    position: fixed;
    bottom: 0;
    left: 50%;
    transform: translate(-50%, 100%);
    width: 80%;
    border-left: 1px solid grey;
    border-top: 1px solid grey;
    border-right: 1px solid grey;
    transition: all .3s;
    height: 80vh;

  }
  .top{
    display: block;
    position: absolute;
    left: 50%;
    top: -10px;
    transform: translate(-50%, -100%);
    cursor: pointer;
    transition: all .3s
  }
  .top.open{
    transform: translate(-50%, -100%) rotate(180deg);
  }
  .logo{
    height: 60vh;
  }
  .prev img, .next img{
    width: 20px;
  }
  .open{
    transform: translate(-50%, 0%)
  }
  .play img{
    width: 50px;
  }
  .pause img{
    width: 30px;
  }
}
</style>
