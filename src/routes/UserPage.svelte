<script>
  export let id;

  let resp = [];
  let name = "";
  fetch("https://godsapi.dallas.workers.dev/user/matches?user_id="+id)
  .then(response => response.json())
  .then(res => {
    resp = res;
  })
  .catch(err => {
    console.log(err);
  });

  fetch("https://godsapi.dallas.workers.dev/user/name?user_id="+id)
  .then(response => response.text())
  .then(res => {
    name = res
  })
  .catch(err => {
    console.log(err);
  });
</script>

<main>
  Name: {name}<br/>
  User: {id} <br/>
  Match History: <br/>
  {#each resp as match}
    {match}<br/>
  {/each}
</main>
