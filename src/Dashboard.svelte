<script>
  import { slide } from 'svelte/transition'
  let timer = false;
  const timingHack = () => {
    setTimeout(() => {
      timer = true;
      console.log("not what u expected huh");
    }, 5000);
  };
  timingHack();
</script>

{#if timer}
  <div transition:slide="{{duration: 2000}}"  class="dash">
    <p class="spiel">
      Hi!👋🏾 I'm Ricardo(he/him), an Artist turned Software Engineer. Here's a link to my <a href="https://docs.google.com/document/d/1lZwzIkmQ9zLCZkBPNV44exDTsqu7yV_jtPvMAEZE7NY/edit?usp=sharing">resume</a>
      and here are links to my <a href="https://github.com/pestoAioli">GitHub</a> and <a href="https://linkedin/in/ricardomiguelriverachavez">LinkedIn</a>. Thanks for stopping by🙏🏽😍 <br>
      Black Lives Matter👊🏿, Trans Lives Matter🏳️‍⚧️, Free Ukraine🇺🇦
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
  .spiel{
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    font-size: 24px;
    opacity: none;
  }
</style>
