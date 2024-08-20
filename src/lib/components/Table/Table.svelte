<script lang="ts">
  import { onMount } from "svelte";

  export let loading = false;
  export let metaData: { total: number; count: number; page: number } = {
    total: 0,
    count: 20,
    page: 1,
  };
  export let bottomLoading = false;
  export let onPageChange: (page: number) => void = () => {};

  const onScroll = (e: any) => {
    if (e?.target) {
      const { scrollTop, scrollHeight, clientHeight } = e.target;

      let percentage = Number(
        (((scrollTop + clientHeight) / scrollHeight) * 100).toFixed(0)
      );

      if (percentage >= 70 && !loading) {
        if (metaData.total / metaData.count > metaData.page && !bottomLoading) {
          onPageChange(metaData.page + 1);
        }
      }

      // if (scrollTop + clientHeight >= scrollHeight - 5 && !loading) {
      //     if (metaData.total / metaData.count > metaData.page) {
      //         onPageChange(metaData.page + 1, searchValue);
      //     }
      // }
    }
  };

  let id = String(Math.floor(Math.random() * 1e10));
  let allowedTags = ["THEAD", "TBODY"];

  function validateSlots() {
    const slotElements = document.querySelectorAll(
      `#table_container_${id} > *`
    );

    slotElements.forEach((element) => {
      if (!allowedTags.includes(element.tagName)) {
        throw new Error(
          `Invalid child element: only <thead> and <tbody> elements are allowed inside Table.`
        );
      }
    });
  }

  onMount(validateSlots);
</script>

<div class="border rounded-lg overflow-auto h-full" on:scroll="{onScroll}">
  <table id="table_container_{id}" class="w-full">
    <slot name="table_head" />
    <slot name="table_body" />
  </table>
</div>
