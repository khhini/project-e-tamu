<script>
  import { user } from "./_store";
  import { onMount } from "svelte";
  var data;
  var url;
  var title;
  var tabelhead;
  
  function getData(url) {
    fetch(url, {
      method: "GET",
      headers: {
        "Content-type": "application/json; charset=UTF-8"
      }
    })
      .then(x => x.json())
      .then(json => {
        data = json;
      })
      .then(() => console.log(data));
  }
  function deleteApi(url){

  }
  
  if ($user["level"] == "admin") {
    url = "http://localhost:5000/user";
    title = "List User";
    tabelhead = ["No", "E-mail", "Nama", "No Hp", "Level", "Aksi"];
  } else if ($user["level"] == "user") {
    url = "http://localhost:5000/event/" + $user._id.$oid;
    title = "List E-Tamu";
    tabelhead = [
      "No",
      "Nama Event",
      "Lokasi Event",
      "Tanggal Event",
      "Jam Mulai",
      "Jam Selesai",
      "Format Form",
      "Aksi"
    ];
  }
  getData(url);
</script>

<div class="card w-100">
  <div class="card-body mx-3">
    <div class="row">
      <h5 class="card-title h1">{title}</h5>
    </div>
    {#if $user['level'] == 'user'}
      <div class="row">
        <a href="/" class="btn btn-primary text-light m-3">+ Buku Tamu</a>
      </div>
    {/if}
    <div class="row" />
    <table class="table">
      <thead class="thead-dark">
        <tr>
          {#each tabelhead as head}
            <th scope="col">{head}</th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#if data && $user['level'] == 'admin'}
          {#each data as d, i}
            <tr>
              <td>{i + 1}</td>
              <td>{d.email}</td>
              <td>{d.nama}</td>
              <td>{d.no_hp}</td>
              <td>{d.level}</td>
              <td>
                <button class="btn btn-warning">
                  <i class="fas fa-edit" />
                </button>
                <button class="btn btn-danger">
                  <i class="fas fa-trash" />
                </button>
              </td>
            </tr>
          {/each}
        {:else if data && $user['level'] == 'user'}
          {#each data as d, i}
            <tr>
              <td>{i + 1}</td>
              <td>{d.nama_event}</td>
              <td>{d.lokasi_event}</td>
              <td>{d.tgl_event}</td>
              <td>{d.jam_mulai}</td>
              <td>{d.jam_selesai}</td>
              <td>{d.format_form}</td>
              <td>
              <button class="btn btn-primary">
                  <i class="fas fa-find" />
                </button>
                <button class="btn btn-warning">
                  <i class="fas fa-edit" />
                </button>
                <button class="btn btn-danger">
                  <i class="fas fa-trash" />
                </button>
              </td>
            </tr>
          {/each}
        {/if}
      </tbody>
    </table>

  </div>
</div>
