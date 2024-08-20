<script>
  import { onMount } from "svelte";

  let id = String(Math.floor(Math.random() * 1e10));
  let allowedTag = "TH";

  function validateSlots() {
    const slotElements = document.querySelectorAll(`#table_head_${id} > *`);

    slotElements.forEach((element) => {
      if (element.tagName !== allowedTag) {
        throw new Error(
          `Invalid child element: only <th> elements are allowed inside TableHead.`
        );
      }
    });
  }

  onMount(validateSlots);
</script>

<thead id="table_head_{id}" class="bg-green-100 sticky top-0">
  <slot />
</thead>
