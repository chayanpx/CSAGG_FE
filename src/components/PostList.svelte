<script>
  import PostForm from "./PostForm.svelte";
  import { user, pages } from "../store.js";
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  const onLogout = () => {
    $user = { username: "" };
    $pages = "Login";
    dispatch("navigate", "right");
  };
</script>

<style>
  .container {
    padding: 0 10rem;
    padding-top: 10rem;
  }
</style>

<div class="container">
  <h1>
    Posts List
    <span>
    <!-- เมื่อ click ให้เรียก function logout -->
      <button style="float:right" class="button-outline" on:click={onLogout}> 
      </button>
    </span>
  </h1>
  <hr />
  <PostForm />
  <slot />
</div>
