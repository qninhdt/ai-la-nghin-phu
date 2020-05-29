
<script>
  export let active = 0
  const list = [...Array(10).keys()].reverse()

</script>

<style>
  .menu li {
    background: #f5f5f5;
    padding: 3px;
    border-radius: 10px;
    text-align: center;
    margin-bottom: 5px;
  }
  .menu li:hover {
    background: #e2e2e2;
  }
  .menu li.active {
    background: #00d1b2;
    color: whitesmoke;
    font-weight: 700;
  }
</style>

<aside class="menu">
  <p class="menu-label">
    Câu hỏi
  </p>
  <ul class="menu-list">
    {#each list as i}
      {#if (i+1) % 3 == 0}
        <hr>
      {/if}
      <li class:active={ active == i }>Câu {i+1}</li>
    {/each}
  </ul>
</aside>