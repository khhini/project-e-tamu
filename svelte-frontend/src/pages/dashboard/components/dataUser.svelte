<script>
  export let data;
  export let i;
</script>

<tr>
  <td>{i + 1}</td>
  <td>{data.email}</td>
  <td>{data.nama}</td>
  <td>{data.no_hp}</td>
  <td>{data.level}</td>
  <td>
    <button class="btn btn-warning">
      <i class="fas fa-edit" />
    </button>
    <button class="btn btn-danger">
      <i class="fas fa-trash" />
    </button>
  </td>
</tr>
