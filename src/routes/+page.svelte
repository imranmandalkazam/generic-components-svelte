<script lang="ts">
  import Table from "$lib/components/Table/Table.svelte";
  import TableBody from "$lib/components/Table/TableBody/TableBody.svelte";
  import TableRow from "$lib/components/Table/TableBody/TableRow.svelte";
  import TableRowCell from "$lib/components/Table/TableBody/TableRowCell.svelte";
  import TableHead from "$lib/components/Table/TableHead/TableHead.svelte";
  import TableHeadCell from "$lib/components/Table/TableHead/TableHeadCell.svelte";

  let table_data: any[] = [1, 2, 3, 4, 5, 6, 7, 8, 8, 1, 2, 2, 3, 2, 1, 1, 1];

  const handleClick = () => {
    console.log("first");
  };
</script>

<section class="p-5 h-[50vh]">
  <Table
    metaData="{{ page: 1, count: 20, total: 300 }}"
    onPageChange="{(page) => {
      console.log(page);
    }}"
  >
    <TableHead slot="table_head">
      <TableHeadCell>
        <input type="checkbox" class="w-10" />abc
      </TableHeadCell>
      <TableHeadCell>abc</TableHeadCell>
      <TableHeadCell>abc</TableHeadCell>
    </TableHead>
    <TableBody {table_data} slot="table_body">
      <TableRow slot="table_body_row" let:data>
        <TableRowCell>
          <input type="checkbox" class="w-10" />
          sjdlkfasldf
        </TableRowCell>
        <TableRowCell>{data}</TableRowCell>
        <TableRowCell>sjdlkfasldf</TableRowCell>
      </TableRow>
    </TableBody>
  </Table>
</section>
