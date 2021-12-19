<script lang="ts">
  import {
    DropdownItem,
    DropdownMenu,
    DropdownToggle,
    Dropdown,
    Input,
  } from "sveltestrap";
  let isOpen = false;

  let input: string;
  let response: any;

  function updateResponse() {
    fetch("https://godsusersearch.dallas.workers.dev?username=" + input)
      .then((response) => response.json())
      .then((data) => {
        response = data;
      })
      .catch((error) => {
        response = error;
      });
  }
</script>

<main>
  <Dropdown {isOpen} toggle={() => (isOpen = !isOpen)}>
    <DropdownToggle tag="div" class="d-inline-block">
      <Input
        bind:value={input}
        on:input={updateResponse}
        placeholder="Enter username..."
      />
    </DropdownToggle>
    <DropdownMenu>
      {#if response && response.length > 0}
        {#each response as doc}
          <DropdownItem href="/user/{doc.user_id}">
            {doc.username}#{doc.user_id} [W: {doc.won_matches} L: {doc.lost_matches}]
          </DropdownItem>
        {/each}
      {/if}
    </DropdownMenu>
  </Dropdown>
</main>
