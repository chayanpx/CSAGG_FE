<script>
  let username = "";
  let password = "";
  let err = "";
  import { pages } from "../store.js";
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  const onLogin = async () => {
    if (!(username && password)) {
      err = "plz check username and password";
      return;
    }
    let res = await fetch("https://malakor.herokuapp.com/api/user", {
      method: "post",
      body: JSON.stringify({ username, password }),
      headers: {
        "content-type": "application/json"
      }
    });
    let text = await res.text();
    if (res.ok) {
      $pages = "Login";
    } else {
      err = text;
    }
  };
  const onCancle = () => {
    $pages = "Login";
    dispatch("navigate", "right");
  };
</script>

<style>
  .container {
    position: relative;
    top: 50%;
    transform: translateY(-50%);
    text-align: center;
    display: block;
  }
  .container input {
    width: 500px;
  }
</style>

<svelte:head>
  <title>Login to forum</title>
</svelte:head>
<section class="container">
  <div>
  <!-- ทำไมค่าไม่เปลี่ยนฟระ -->
    <input bind:value={username} type="text" placeholder="username" />
  </div>
  <div>
  <!-- นี่ด้วย -->
    <input bind:value={password} type="password" placeholder="password" />
  </div>
  <p style="color:red">{err}</p>
  <button class="button button-outline" on:click={onLogin}>Registor</button>
  <button class="button button-clear" on:click={onCancle}>Back</button>
</section>
