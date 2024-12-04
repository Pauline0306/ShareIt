<script>
    import './Homepage.css';
    import { onMount } from 'svelte';
    import { goto } from '$app/navigation';
    
    let searchTerm = '';
    let filteredPosts = [];
    let posts = []; // Fetch or pass posts data
    let isVisible = false;
    let selectedPost = null;
    let comments = [];
    let newComment = '';
    
    function filterPosts() {
      filteredPosts = posts.filter(post => post.user_fullname.toLowerCase().includes(searchTerm.toLowerCase()));
    }
    
    function truncateText(text, length) {
      return text.length > length ? text.substring(0, length) + '...' : text;
    }
    
    function viewPost(id) {
      selectedPost = posts.find(post => post.id === id);
      isVisible = true;
    }
    
    function closeModal() {
      isVisible = false;
    }
    
    function addComment(postId) {
      comments.push({ comment: newComment });
      newComment = '';
    }
    
    onMount(() => {
      filterPosts();
    });
  </script>
  
  <div class="header">
    <nav class="topnav">
      <div class="upper-header">
        <h1 style="font-family: Georgia, serif;">PixelMinds</h1>
        <button on:click={() => goto('/login')} style="font-family: Georgia, serif;">Login / Signup</button>
      </div>
    </nav>
  </div>
  
  <div class="search-container">
    <input type="text" placeholder="Search by author's name..." bind:value={searchTerm} on:input={filterPosts}>
  </div>
  
  <div class="feed-container">
    <div class="ads">
      <div class="about-div">
        <div class="about-title"></div>
        <div class="about-desc">
          <img src="image.jpg" alt="Descriptive text">
          <div class="overlay-text">
            <p>
              Welcome to PixelMinds, the ultimate platform for writers, thinkers, and creators to share their thoughts.
              Our user-friendly interface and powerful tools make it easy for you to craft compelling blog posts,
              connect with like-minded individuals, and grow your audience.
            </p>
          </div>
        </div>
      </div>
    </div>
  
    <div class="feed-posts">
      {#each filteredPosts as post}
        <div class="feed-item">
          <img src={post.image ? post.image : '/assets/ccs.jpg'} alt="Post Image">
          <div class="feed-holder">
            <div class="feed-header">
              <div class="author-info">
                <div class="profile-pic-container"></div>
                <p id="fullname">{post.user_fullname}</p>
                <p id="date">{new Date(post.created_at).toLocaleString()}</p>
              </div>
            </div>
            <div class="feed-body">
              <p class="post-title">{post.title}</p>
              <hr />
              <p class="post-content">{truncateText(post.content, 100)}</p>
            </div>
          </div>
          <button type="button" on:click={() => viewPost(post.id)}>Read More</button>
        </div>
      {/each}
    </div>
  </div>
  
  {#if isVisible}
    <div class="modal">
      <div class="modal-content">
        <span class="close-button" on:click={closeModal}>&times;</span>
        <div class="modal-image">
          <img src={selectedPost?.image ? selectedPost.image : '/assets/ccs.jpg'} alt="Post Image">
        </div>
        <h2 style="color: #4f3b78;">{selectedPost?.title}</h2>
        <p>{@html selectedPost?.content}</p>
  
        <div class="comment-section">
          <h3>Comments</h3>
          <div class="comments-display">
            {#each comments as comment}
              <div class="comment">
                <span class="comment-user">{comment.comment}</span>
              </div>
            {/each}
          </div>
          <div class="comment-input">
            <input type="text" bind:value={newComment} placeholder="Add a comment...">
            <button on:click={() => addComment(selectedPost.id)} class="submit-comment">Post</button>
          </div>
        </div>
      </div>
    </div>
  {/if}
  