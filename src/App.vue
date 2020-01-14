<template>
  <div id="app">
    <header>
      <h2>Rockify By Saad Ayouj </h2>
      
    </header>
    <main>
      <section class="player">
        <h2 class="song-title">{{ current.title }} - <span>{{ current.artist }}</span></h2>
        <div class="controls">
          <button class="prev" @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
      </section>
      <section class="playlist">
        <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src == current.src) ? 'song playing' : 'song'">
          {{ song.title }} - {{ song.artist }}
        </button>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
        title: 'Thunderstruck',
        artist: 'AC/DC',
        src: require('./assets/DC - Thunderstruck.mp3')
        },
        {
          title: 'Teutonic Terror',
          artist: 'ACCEPT',
          src: require('./assets/ACCEPT - Teutonic Terror.mp3')
        },
        {
        title: 'Back In The Game',
        artist: 'Airbourne',
        src: require('./assets/Airbourne - Back In The Game [OFFICIAL VIDEO].mp3')
        },
        {
        title: 'Live It Up',
        artist: 'Airbourne',
        src: require('./assets/Airbourne - Live It Up (Official Video).mp3')
        }
      ],
      player: new Audio()
    }
  },
  methods: {
    play (song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.player.addEventListener('ended', function () {
        this.index++;
        if (this.index > this.songs.length - 1) {
          this.index = 0;
        }
        this.current = this.songs[this.index];
        this.play(this.current);
      }.bind(this));
      this.isPlaying = true;
    },
    pause () {
      this.player.pause();
      this.isPlaying = false;
    },
    next () {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    prev () {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    }
  },
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  }
}
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}
body {
  font-family: sans-serif;
  cursor: url('./assets/bass.png'),pointer;
  background-image: url('./assets/concert.jpg');
  background-size: cover;
  background-repeat: no-repeat;
}
header {
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 15px;
  background-image: linear-gradient(to right, rgba(44, 0, 0, 0.801), rgb(32, 31, 31));
	color: #FFF;
}
main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}
.song-title {
  color: whitesmoke;
  font-size: 30px;
  font-weight: 600;
  text-transform: uppercase;
  text-align: center;
  background-color: rgba(24, 22, 22, 0.692);
  padding: 10px;
  border-radius: 12px;
}
.song-title span {
  font-weight: 400;
  font-style: italic;
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
  cursor: url('./assets/festival.png'),pointer;
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
  background-color: rgba(0, 0, 0, 0.822);
}
.next, .prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #FFF;
  background-color: rgba(90, 90, 90, 0.911);
}
.playlist {
  padding: 0px 30px;
}
.playlist .song {
  display: block;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  font-weight: 700;
  cursor: url('./assets/guitar.png'),pointer;
  color: whitesmoke;
}
.playlist .song:hover {
  color: rgb(97, 0, 0);
}
.playlist .song.playing {
  color: rgba(226, 221, 221, 0.74);
  background-image: linear-gradient(to right, rgb(27, 13, 17), rgb(54, 54, 54));
}
</style>
      
