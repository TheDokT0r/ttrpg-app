<script lang="ts">
  import "./global.scss";
  import Sheet from "./Pages/ChracterSheet/Sheet.svelte";
  import { getApp, initializeApp } from "firebase/app";
  import { getAuth } from "firebase/auth";
  import Login from "./Pages/Login.svelte";
  import { SvelteToast } from "@zerodevx/svelte-toast";
  import { Router, Route, navigate } from "svelte-routing";

  export let url: string = "";

  const app = getApp();
  const auth = getAuth(app);

  auth.onAuthStateChanged(() => {
    if (!auth.currentUser) {
      navigate("/login", { replace: true });
    } else {
      navigate("/", { replace: true });
    }
  });
</script>

<Router {url}>
  <svelte:fragment>
    <Route path="/"><Sheet /></Route>
    <Route path="login"><Login {app} /></Route>
  </svelte:fragment>
</Router>

<SvelteToast />
