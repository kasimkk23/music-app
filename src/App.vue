<template>
  <div id="app" @mousemove="mousemove">
    <header>
      <h1>Music App</h1>
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }}</h2>
        <h3 class="song-artist"> {{ current.artist }}</h3>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
    </main>
    <section class="playlist">
        <h3>The Playlist</h3>
        <button 
        v-for="song in songs" 
        :key="song.src" 
        @click="play(song)" 
        :class="(song.src == current.src) ? 'song playing' : 'song'">
          {{ song.title }} - {{ song.artist }}
        </button>
      </section>

      <section class="main-artist">
        <div class="artist">
          <Artist 
          v-for="artist in artists"
          :key="artist.color"
          :artist="artist"
          />
        </div>
      </section>
  </div>
</template>

<script>
import Artist from './components/Artist';
export default {
  name: 'App',
  components: {
    Artist
  },
  data () {
    return {
      artists:[
        {
          title: 'Adele',
          color: 'green',
          bgtext: 'A D L',
          src: require('./assets/adele.png')
        },
        {
          title: 'Lyna',
          color: 'blue',
          bgtext: 'L Y N',
          src: require('./assets/lyna.png')
        },
        {
          title: 'TOM',
          color: 'pink',
          bgtext: 'TOM',
          src: require('./assets/saymyname.png')
        }
      ],





      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Maa',
          artist: 'kasim',
          src: require('./assets/maa.mp3')
        },
        {
          title: 'Yeh hai meri kahani',
          artist: 'kasim',
          src: require('./assets/kahani.mp3')
        }
      ],
      player: new Audio(),
    }
  },
  methods: {
    play (song) {
      if(typeof song.src != "undefined"){
        this.current = song;
        this.player.src = this.current.src;
      }
        this.player.play();
        this.isPlaying =true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    },
    next () {
      this.index++;
      if(this.index > this.songs.length - 1){
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev () {
      this.index--;
      if(this.index < 0){
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    mousemove(e) {
      let mouseX = e.mouseX;
      let mouseY = e.mouseY;

      let artists = document.querySelectorAll('.artists .artist');
      for(let a = 0; a < artists.length; ++a){
        let artist = artists[a];

        let artist_image = artist.querySelector('.artist-image-wrap');

        let img_x = mouseX - this.coords(artist_image).x;
        let img_y = mouseY - this.coords(artist_image).y;

        artist_image.style.transform = `translateY(-${img_y/20}px) translateX(-${img_x/20}px) translateZ(100px)`;
        let bgtext = artist.querySelector('.bg-text');
        let bg_x = mouseX - this.coords(bgtext).x;
        bgtext.style.transform = `translateX(${bg_x/25}px)`;
      }
    },
    coords (el) {
      let coords = el.getBoundingClientRect();
      return {
        x: coords.left / 2,
        y: coords.top / 2
      }
    }
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
    //this.player.play();
  }
}
</script>




<style>
*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
body{
  /* background: #dfe7ef; */
  background-repeat: repeat;
  font-family: 'Open Sans', 'Helvetica Neue', sans-serif;
}
header {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 15px;    
  background-color: #8c306b;
  color: #ffeaea;
}
#app {
  background-image: url('./assets/warm-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4 ease;
  min-height: 100vh;
}
main {
  
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.2), rgba(0, 0, 0, 0.75));
  padding: 25px;
}

.song-title {
  color: #b9719f;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.song-title span {
  font-weight: 400;
  font-style: italic;
}

.song-artist {
  color: #dc77b8;
  font-size: 20px;
  font-weight: 400;
  text-align: center;
}

.controls {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 30px 15px;
}
button {
  appearance: none;
  background: none;
  border: none;
  outline: none;
  cursor: pointer;
}
button:hover {
  opacity: 0.8;
}
.play, .pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #FFF;
  background-color: #471e4f;
}
.next, .prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #FFF;
  background-color: #8b316b;
}
.playlist {
  padding: 0px 30px;
}
.playlist h3 {
  color: #212121;
  font-size: 28px;
  font-weight: 400;
  margin-bottom: 30px;
  text-align: center;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: pointer;
}
.playlist .song:hover {
  color: #FF5858;
}
.playlist .song.playing {
  color: #FFF;
  background-image: linear-gradient(to right, #8c306b, #8a2f5a);
}

.main-artist {
  width: 100vw;
  background-color:#bb408b;
  display: flex;
  justify-content: center;
  align-items: center;
}
.artist{
  font-size: 18px;
  color:#FFF;
  display: flex;
  max-width: 1280px;
  padding: 25px;
  margin: 0 auto;
}
</style>
