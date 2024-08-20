<script>
  import { onMount } from "svelte";

  let id = String(Math.floor(Math.random() * 1e10));
  let allowedTag = "TD";

  function validateSlots() {
    const slotElements = document.querySelectorAll(`#table_row_${id} > *`);

    slotElements.forEach((element) => {
      if (element.tagName !== allowedTag) {
        throw new Error(
          `Invalid child element: only <td> elements are allowed inside TableRow.`
        );
      }
    });
  }

  onMount(validateSlots);
</script>

<tr id="table_row_{id}">
  <slot />
</tr>
