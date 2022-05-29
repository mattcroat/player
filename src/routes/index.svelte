<script lang="ts">
  import Playlist from '$lib/playlist.svelte'
  import Player from '$lib/player.svelte'

  const tracks = [
    {
      title: 'Track 1',
      album: 'Album',
      duration: '2:00',
    },
    {
      title: 'Track 2',
      album: 'Album',
      duration: '2:00',
    },
    {
      title: 'Track 3',
      album: 'Album',
      duration: '2:00',
    },
    {
      title: 'Track 4',
      album: 'Album',
      duration: '2:00',
    },
  ]

  let playing = false
  let songPlayingIndex = 0
  let numberOfTracks = tracks.length - 1
  let shuffle = false
  let repeat: 'none' | 'playlist' | 'track' = 'none'

  function setPlaying(): void {
    playing = !playing
  }

  function playTrack(): void {
    playing = true
  }

  function pauseTrack(): void {
    playing = false
  }

  function setSongPlayingIndex(index: number): void {
    songPlayingIndex = index
  }

  function setShuffle() {
    shuffle = !shuffle
  }

  function setRepeat() {
    switch (repeat) {
      case 'none':
        repeat = 'playlist'
        break
      case 'playlist':
        repeat = 'track'
        break
      case 'track':
        repeat = 'none'
    }
  }

  $: console.log({ playing, songPlayingIndex, shuffle, repeat })
</script>

<Playlist
  {tracks}
  {playing}
  {playTrack}
  {pauseTrack}
  {songPlayingIndex}
  {setSongPlayingIndex}
/>
<Player
  {playing}
  {setPlaying}
  {songPlayingIndex}
  {setSongPlayingIndex}
  {numberOfTracks}
  {shuffle}
  {setShuffle}
  {repeat}
  {setRepeat}
/>
