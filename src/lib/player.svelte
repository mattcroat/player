<script lang="ts">
  export let playing: boolean
  export let setPlaying: () => void

  export let songPlayingIndex: number
  export let setSongPlayingIndex: (index: number) => void

  export let numberOfTracks: number

  export let shuffle: boolean
  export let setShuffle: () => void

  export let repeat: 'none' | 'playlist' | 'track'
  export let setRepeat: () => void

  function randomIndex() {
    return Math.ceil(Math.random() * numberOfTracks)
  }

  function playTrack() {
    if (!playing && !songPlayingIndex) {
      shuffle ? setSongPlayingIndex(randomIndex()) : setSongPlayingIndex(0)
    }
    setPlaying()
  }

  function previousTrack() {
    if (!playing || songPlayingIndex <= 0) return

    shuffle
      ? setSongPlayingIndex(randomIndex())
      : setSongPlayingIndex((songPlayingIndex -= 1))
  }

  function nextTrack() {
    if (!playing || songPlayingIndex >= numberOfTracks) return

    shuffle
      ? setSongPlayingIndex(randomIndex())
      : setSongPlayingIndex((songPlayingIndex += 1))
  }
</script>

<button on:click={setShuffle}>
  {shuffle ? 'Shuffle On' : 'Shuffle'}
</button>

<button on:click={previousTrack}>Previous</button>

<button on:click={playTrack}>
  {!playing ? 'Play' : 'Pause'}
</button>

<button on:click={nextTrack}>Next</button>

<button on:click={setRepeat}>
  {repeat === 'none' ? 'Repeat' : `Repeat ${repeat}`}
</button>
