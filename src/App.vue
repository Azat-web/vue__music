<template>
  <div id="app">
    <div class="container">
      <header>
        <h1 class="header__title">Music cloud</h1>
      </header>
      <main>
        <div class="player">
          <h2 class="player__song-title">
            {{ current.title }} - {{ current.artist }}
          </h2>
          <div class="player__controls">
            <button class="player__controls-prev" @click="prev">Назад</button>
            <button
              class="player__controls-play"
              v-if="!isPlaying"
              @click="play"
            >
              Играть
            </button>
            <button class="player__controls-pause" v-else @click="pause">
              Пауза
            </button>
            <button class="player__controls-next" @click="next">Вперед</button>
          </div>
        </div>
        <div class="playlist">
          <h3 class="playlist__title">Плейлист</h3>
          <button
            v-for="song in songs"
            :key="song.src"
            @click="play(song)"
            :class="song.src === current.src ? 'song playing' : 'song'"
          >
            {{ song.title }} - {{ song.artist }}
          </button>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data: () => ({
    current: {},
    index: 0,
    isPlaying: false,
    songs: [
      {
        title: "SmK",
        artist: "Celestial",
        src: require("./assets/Celestial.mp3"),
      },
      {
        title: "Enigms",
        artist: "Dreams",
        src: require("./assets/Dreams.mp3"),
      },
      {
        title: "Ach",
        artist: "Hello, Karle...",
        src: require("./assets/Karle.mp3"),
      },
      {
        title: "Enigma",
        artist: "Rock Bottom",
        src: require("./assets/Rock-Bottom.mp3"),
      },
      {
        title: "SmK",
        artist: "Reactive",
        src: require("./assets/Reactive.mp3"),
      },
    ],
    player: new Audio(),
  }),
  methods: {
    play(song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
      }
      this.player.play();
      this.isPlaying = true;
    },
    pause() {
      this.player.pause(), (this.isPlaying = false);
    },
    prev() {
      this.index--;
      if (this.index < 0) {
        this.index = this.songs.length - 1;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
    next() {
      this.index++;
      if (this.index > this.songs.length - 1) {
        this.index = 0;
      }
      this.current = this.songs[this.index];
      this.play(this.current);
    },
  },
  created() {
    this.current = this.songs[this.index];
    this.player.src = this.current.src;
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  min-width: 400px;
}

.container {
  background: no-repeat center/120% url("../public/bg5.jpg");
  height: 110vh;
}

header {
  display: flex;
  justify-content: left;
  align-items: center;
  padding: 15px 40px;
  background-color: #212121;
  color: rgb(233, 104, 104);
}

main {
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  padding: 25px;
}

.player__song-title {
  color: #d3778b;
  font-size: 32px;
  font-weight: 700;
  text-transform: uppercase;
  text-align: center;
}
.player__song-title span {
  font-weight: 400;
  font-style: italic;
}
.player__controls {
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
.player__controls-play,
.player__controls-pause {
  font-size: 20px;
  font-weight: 700;
  padding: 15px 25px;
  margin: 0px 15px;
  border-radius: 8px;
  color: #fff;
  background-color: #cc2e5d;
}
.player__controls-next,
.player__controls-prev {
  font-size: 16px;
  font-weight: 700;
  padding: 10px 20px;
  margin: 0px 15px;
  border-radius: 6px;
  color: #fff;
  background-color: #ff5858;
}
.playlist {
  padding: 0px 30px;
}

.playlist h3 {
  color: #dbd4d4;
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
  color: #fff;
}
.playlist .song:hover {
  color: #ff5858;
}
.playlist .song.playing {
  color: #fff;
  background-image: linear-gradient(to right, #cc2e5d, #ff5858);
}

@media (min-width: 400px) {
  .container {
    background: no-repeat url("../public/bg5.jpg");
    height: 110vh;
  }
}
</style>
