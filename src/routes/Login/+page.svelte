<script>
    import './Login.css';
    import { Link } from 'svelte-routing';

let email = '';
let password = '';
let errorMessage = '';
let isSubmitting = false;

const handleSubmit = () => {
  errorMessage = '';

  // Simple validation
  if (!email || !password) {
    errorMessage = 'Both fields are required.';
    return;
  }

  // Simulate login action (replace with API call)
  isSubmitting = true;
  setTimeout(() => {
    isSubmitting = false;
    if (email === 'test@example.com' && password === 'password') {
      // Simulate successful login
      alert('Login successful!');
    } else {
      // Simulate a failed login attempt
      errorMessage = 'Invalid email or password.';
    }
  }, 1000);
};
</script>

<div id="login-container">
<div class="p-5">
  <h3>Login</h3>
  <h5>Welcome Back</h5>
  <p>Please enter your email and password</p>
  <div>
    <label for="email">Email</label>
    <input
      type="text"
      id="email"
      placeholder="Enter your email"
      bind:value={email}
    />
  </div>
  <div>
    <label for="password">Password</label>
    <input
      type="password"
      id="password"
      placeholder="Enter your password"
      bind:value={password}
    />
  </div>
  {#if errorMessage}
    <div class="error-message">{errorMessage}</div>
  {/if}
  <button
    class="btn"
    on:click={handleSubmit}
    disabled={isSubmitting}
  >
    {#if isSubmitting}
      <span class="loading">Logging in...</span>
    {:else}
      Login
    {/if}
  </button>

  <p class="text-muted"> Don't have an account?
     <a href="/Register" id="register-route">Register</a>
  </p>
</div>
</div>
