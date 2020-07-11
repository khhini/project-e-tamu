<script>
  import { goto, url } from "@sveltech/routify";
  import { user } from "./_store";

  $: if (!sessionStorage.getItem("user")) {
    $goto("/login", {}, false);
  }
  function logout() {
    $user = false;
    sessionStorage.clear();
    $goto("/", {}, false);
  }

  $user = JSON.parse(sessionStorage.getItem("user"));
</script>

<nav class="navbar navbar-expand-lg navbar-light bg-warning">
  <div class="container">
    <a class="navbar-brand" href={$url('./')}>E-Tamu</a>

      <div class="btn-group">
        <button
          type="button"
          class="btn btn-success dropdown-toggle"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false">
          {$user['nama']}
        </button>
        <div class="dropdown-menu">
          <a class="dropdown-item" href="{$url('./profile')}">Profile</a>
          <div class="dropdown-divider" />
          <button type="button" class="dropdown-item bg-danger text-light" on:click="{logout}">Logout</button>
        </div>
      </div>
    
  </div>
</nav>
<div class="container mt-3">
  <slot />
</div>
