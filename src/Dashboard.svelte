<script>
  import { slide } from 'svelte/transition'
  let timer = false;
  const timingHack = () => {
    setTimeout(() => {
      timer = true;
    }, 1500);
  };
  timingHack();

  let open = false;

  const handleOpen = () => {
  open = true;
  timer = false;
  }

</script>

{#if timer}
<button transition:slide="{{duration: 1200}}" class="boop" >
  <p class="spiel" on:click={handleOpen}>ℹ</p>
</button>
{/if}
{#if open}
<div transition:slide="{{duration: 2000}}"  class="dash">
  <p class="spiel">
    Hi!👋🏾 I'm Ricardo(he/him), an Artist and Software Engineer. Here's a link to my <a href="https://docs.google.com/document/d/1lZwzIkmQ9zLCZkBPNV44exDTsqu7yV_jtPvMAEZE7NY/edit?usp=sharing">resume</a>
    and here are links to my <a href="https://github.com/pestoAioli">GitHub</a> and <a href="https://linkedin.com/in/ricardomiguelriverachavez">LinkedIn</a>. Thanks for stopping by🙏🏽😍 P.S drag the screen around to move the camera🎥😀
  </p>
</div>  
{/if}

<style>
  .dash {
    display: flex;
    justify-content: center;
    position: relative;
    background-color: rgba(96, 224, 147, 0.643);
    padding: 25px 25px;
    width: 50vw;
    border-radius: 6px;
    top: 5vh;
    left: 5vw;
  }
  .boop {
    display: flex;
    justify-content: center;
    position: relative;
    background-color: rgba(96, 224, 147, 0.95);
    padding: 15px;
    width: 5vw;
    border-radius: 6px;
    top: 5px;
    left: 5vw;
    cursor: pointer;
  }
  .spiel{
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 24px;
    opacity: none;
  }

  @media screen and (max-width: 300px) {
    .spiel{
      font-size: 16px;
    }
  }
</style>
