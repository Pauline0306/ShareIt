<script>
    import './Register.css';
    import { Link } from 'svelte-routing';

   let user_fullname = '';
   let user_email = '';
   let password = '';
   let errorMessage = '';
 
   const onSubmit = () => {
     // Add your form submission logic here
     if (!user_fullname || !user_email || !password) {
       errorMessage = 'All fields are required.';
       return;
     }
     alert('Form Submitted!');
   };
 
   const Login = () => {
     // Navigate to the login page (you can use Svelte's routing)
     // For SvelteKit: use navigate() or href
     window.location.href = '/Login'; // Use SvelteKit's navigation if needed
   };
 </script>

<div class="container">
   <div class="register-container">
     <div class="card border-0">
       <div class="card-body p-0">
         <div class="p-5">
           <div class="mb-5">
             <h3 class="h4 font-weight-bold">  Register New User </h3>
           </div>
           <form on:submit|preventDefault={onSubmit}>
             <div class="form-group">
               <label for="fullname">Full Name</label>
               <input
                 type="text"
                 class="form-control"
                 id="fullname"
                 bind:value={user_fullname}
                 name="fullname"
                 required
                 placeholder="Enter your Full Name"
                 autocomplete="off"
               />
             </div>
             <div class="form-group">
               <label for="email">Email</label>
               <input
                 type="email"
                 class="form-control"
                 id="email"
                 bind:value={user_email}
                 name="email"
                 required
                 placeholder="Enter your Email"
                 autocomplete="off"
               />
             </div>
             <div class="form-group mb-5">
               <label for="password">Password</label>
               <input
                 type="password"
                 class="form-control"
                 id="password"
                 bind:value={password}
                 name="password"
                 required
                 placeholder="Enter your Password"
                 autocomplete="off"
               />
             </div>
             <button type="submit" class="btn">Create Account</button>
           </form>
           <p class="text-muted text-center mt-4">  Already registered?
             <a class="ml-1"id="login-route"on:click={Login}  >Return to Login</a>
           </p>
         </div>
       </div>
     </div>
   </div>
 </div>