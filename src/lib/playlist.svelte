<script lang="ts">
  interface Track {
    title: string
    album: string
    duration: string
  }

  export let tracks: Track[]

  export let playing: boolean
  export let playTrack: () => void
  export let pauseTrack: () => void

  export let songPlayingIndex: number
  export let setSongPlayingIndex: (index: number) => void

  let selectedTrack: number

  function setSelectedTrack(trackIndex: number): void {
    selectedTrack = trackIndex
  }

  function setPlay(trackIndex: number, isPlaying: boolean): void {
    if (!isPlaying) {
      playTrack()
      setSongPlayingIndex(trackIndex)
    } else {
      pauseTrack()
    }
  }
</script>

<div class="playlist">
  <div class="labels">
    <div>#</div>
    <div>Title</div>
    <div>Album</div>
    <div>Duration</div>
  </div>

  <ul>
    {#each tracks as track, trackIndex}
      {@const hovered = selectedTrack === trackIndex}
      {@const isPlaying = playing && songPlayingIndex === trackIndex}

      <li
        on:mouseenter={() => setSelectedTrack(trackIndex)}
        on:mouseleave={() => setSelectedTrack(-1)}
        class:isPlaying
      >
        <div class="track">
          {#if !hovered}
            {trackIndex + 1}
          {/if}

          {#if hovered}
            <button on:click={() => setPlay(trackIndex, isPlaying)}>
              {isPlaying ? 'Pause' : 'Play'}
            </button>
          {/if}
        </div>
        <div class="title">{track.title}</div>
        <div class="album">{track.album}</div>
        <div class="duration">{track.duration}</div>
      </li>
    {/each}
  </ul>
</div>

<style>
  .playlist {
    font-family: sans-serif;
  }

  .labels {
    display: flex;
    justify-content: space-between;
    padding: 1rem;
    font-weight: 700;
    border-bottom: 1px solid gainsboro;
  }

  ul {
    margin: 0;
    padding: 0;
  }

  li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
  }

  li:nth-child(even) {
    background-color: gainsboro;
  }

  li.isPlaying {
    background-color: palegreen;
  }

  .track {
    width: 32px;
    height: 32px;
    display: grid;
    place-content: center;
  }

  .title {
    font-weight: 700;
  }
</style>
