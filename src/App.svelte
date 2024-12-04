<script>
    import { Router, Route, Link } from "svelte-routing";
    import Login from './components/Login.svelte';
    import Register from './components/Register.svelte';
    import Homepage from './components/Homepage.svete';
  </script>
  
  
    <nav>
      <Link to="/Homepage">Homepage</Link>
      <Link to="/Login">Login</Link>
      <Link to="/Register">Register</Link>
    </nav>

    <Router>
    <Route path="/Homepage" component={Homepage} />
    <Route path="/Login" component={Login} />
    <Route path="/Register" component={Register} />
  </Router>
  
  <script>
  import { onMount } from 'svelte';
  import Sidenav from './Sidenav.svelte';
  import Body from './Body.svelte';
  import CreatePost from './CreatePost.svelte';

  let isSideNavCollapsed = false;
  let screenWidth = window.innerWidth;
  let modalService = { showModal: false };

  // Function to determine if the side nav should be shown
  const shouldShowSideNav = () => screenWidth > 768;

  // Function to handle the side nav toggle
  const onToggleSideNav = (event) => {
    isSideNavCollapsed = event;
  };

  // Update screen width on window resize
  onMount(() => {
    const updateScreenWidth = () => {
      screenWidth = window.innerWidth;
    };
    window.addEventListener('resize', updateScreenWidth);
    return () => window.removeEventListener('resize', updateScreenWidth);
  });
</script>

{#if shouldShowSideNav()}
  <Sidenav on:toggleSideNav={onToggleSideNav} />
{/if}

<Body 
  {isSideNavCollapsed} 
  {screenWidth} 
  fullWidth={!shouldShowSideNav()} 
/>

{#if modalService.showModal}
  <CreatePost />
{/if}
