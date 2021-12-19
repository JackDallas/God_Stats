<script lang="ts">
  import { Styles } from "sveltestrap";
  import { Container, Nav, Navbar } from "sveltestrap";

  import { Router, Link, Route } from "svelte-routing";
  import Home from "./routes/Home.svelte";
  import UserPage from "./routes/UserPage.svelte";

  import UserSearchBox from "./components/UserSearchBox.svelte";

  export let url = "";
</script>

<Styles />

<Container color="dark">
  <Router {url}>
    <nav>
      <Navbar color="dark" dark>
        <Nav navbar>
          <Link to="/">Home</Link>
          <UserSearchBox />
        </Nav>
      </Navbar>
    </nav>
    <div>
      <Route path="user/:id" let:params>
        <UserPage id={params.id} />
      </Route>
      <Route path="/">
        <Home />
      </Route>
    </div>
  </Router>
</Container>
