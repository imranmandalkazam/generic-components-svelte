<script lang="ts">
  import { onMount } from "svelte";

  type T = $$Generic<{}>;
  export let table_data: T[] = [];

  let id = String(Math.floor(Math.random() * 1e10));
  let allowedTag = "TR";

  function validateSlots() {
    const slotElements = document.querySelectorAll(`#table_body_${id} > *`);

    slotElements.forEach((element) => {
      if (element.tagName !== allowedTag) {
        throw new Error(
          `Invalid child element: only <tr> elements are allowed inside TableBody.`
        );
      }
    });
  }

  onMount(validateSlots);
</script>

<tbody id="table_body_{id}">
  {#each table_data as data}
    <slot name="table_body_row" {data} />
  {/each}
</tbody>
