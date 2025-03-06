<template>
    <nav class="navbar">
      <div class="logo">
        <img 
          src="https://github.com/rainvp/Personal-Profile-Webpage/blob/main/images/logo.png?raw=true"
          alt="Rain's Cafe Logo">
      </div>     
  
    <div class="nav-links">
      <router-link to="/" class="nav-link"><b>Home</b></router-link>
      <router-link to="/resume" class="nav-link"><b>More</b></router-link>
      <router-link to="/gallery" class="nav-link"><b>Gallery</b></router-link>
      <router-link to="/contact" class="nav-link"><b>Contact</b></router-link>
        <div class="dropdown">
            <button class="dropbtn">
                <span class="dropdown-icon">&#x25BC;</span>
            </button>
            <div class="dropdown-content">
                <div class="dropdown-section">
                  <h4 class="dropdown-title">Menu</h4>
                  <router-link to= "/resources">Resources</router-link>
                </div>
                <div class="dropdown-section">
                  <h4 class="dropdown-title">Social</h4>
                  <a href="https://www.facebook.com/raincelannesophia.presa" target="_blank" rel="noopener noreferrer">Facebook</a>
                  <a href="https://www.instagram.com/iamrainvp/" target="_blank" rel="noopener noreferrer">Instagram</a>
                  <a href="https://open.spotify.com/user/31a33al3euch4q3nivqduvjf73aa?si=a31c2d833dd74199" target="_blank" rel="noopener noreferrer">Spotify</a>

                </div>
            </div>
        </div>
    </div> 
  </nav>

    <br>
  
    <!-- Banner Section -->
    <header id="banner">
        <div id="banner-content" class="row clearfix">
            <div class="col-38">
                <div class="section-heading">
                    <h1>Capture & Connect</h1>
                </div>
            </div>
        </div>
    </header>

<!-- Section Title (Properly Positioned) -->

<!-- Gallery Container -->
<div class="gallery-container" data-aos="fade-up">
  <h5 class="tag">Camera Crumbs 📸🍪</h5>
  <div class="gallery-slider">
    <button class="slider-nav left-arrow" @click="prevSlide">&#10094;</button>
    <div class="slider-images-wrapper">
      <div v-for="image in currentImages" :key="image.id" class="slider-image">
        <img :src="image.src" class="gallery-img" />
      </div>
    </div>
    <button class="slider-nav right-arrow" @click="nextSlide">&#10095;</button>
  </div>

  <!-- Caption Below the Slider -->
  <div class="slider-caption">
    <p>{{ currentCaption }}</p>
  </div>
</div>

<br>
<br>

<div id="app">
    <div id="app-comments" class="comments-section" data-aos="zoom-in-up">
      <h2 class="section-title">Share your thoughts!💬</h2>

      <form @submit.prevent="addComment" class="comment-form">
        <input v-model="newComment.name" type="text" placeholder="Your Name" required />
        <textarea v-model="newComment.comment" placeholder="Write a comment..." required></textarea>
        <button type="submit">Post Comment</button>
      </form>

      <div class="comments-list">
        <div v-for="comment in comments" :key="comment.id" class="comment-box">
          <p><strong>{{ comment.name }}</strong>: {{ comment.comment }}</p>
          <span>{{ formatTimestamp(comment.created_at) }}</span>
          
          <a @click="toggleReplyForm(comment.id)" class="reply-trigger">Reply</a>
          
          
          <div v-if="replyForms[comment.id]" class="reply-form">
  <input v-model="newReply[comment.id]" type="text" placeholder="Write a reply..." required />
  <button @click="addReply(comment.id)">Post Reply</button>
</div>

          
          <div v-if="comment.replies.length" class="replies-list">
            <div v-for="reply in comment.replies" :key="reply.id" class="reply-box">
              <p><strong>{{ reply.name }}</strong>: {{ reply.comment }}</p>
              <span>{{ formatTimestamp(reply.created_at) }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, computed } from 'vue';
import supabase from '../lib/supabaseClient';

export default {
  setup() {
    const comments = ref([]);
    const newComment = ref({ name: '', comment: '' });
    const replyForms = ref({});
    const newReply = ref({});
    const userName = ref(null); // Store user's name if they are in guestbook
    const storedEmail = localStorage.getItem("user_email") || null;

    // Fetch user's name from guestbook
    const fetchGuestbookName = async () => {
      if (!storedEmail) return;
      try {
        let { data, error } = await supabase
          .from('guestbook')
          .select('name')
          .eq('email', storedEmail)
          .single();
        
        if (!error && data) {
          userName.value = data.name; // Store user's name
        }
      } catch (err) {
        console.error("Error fetching guestbook name:", err);
      }
    };

    const fetchComments = async () => {
      try {
        let { data, error } = await supabase
          .from('comments')
          .select('*, replies:replies(*)')  
          .order('created_at', { ascending: false });

        if (error) throw error;
        comments.value = data.map(comment => ({ ...comment, replies: comment.replies || [] }));
      } catch (err) {
        console.error("Error fetching comments:", err);
      }
    };

    const addComment = async () => {
  let commentCount = parseInt(localStorage.getItem("comment_count")) || 0;
  let firstCommentTime = localStorage.getItem("first_comment_time");

  const now = new Date().getTime();
  const cooldownDuration = 1800000; // 30 minutes in milliseconds

  // Reset counter if more than 30 minutes have passed since the first comment
  if (firstCommentTime && now - parseInt(firstCommentTime) >= cooldownDuration) {
    localStorage.setItem("comment_count", "0");
    localStorage.setItem("first_comment_time", now.toString());
    commentCount = 0;
  }

  if (commentCount >= 3) {
    alert("You can only post 3 comments every 30 minutes.");
    return;
  }

  if (!newComment.value.name || !newComment.value.comment) return;

  try {
    let { data, error } = await supabase
      .from('comments')
      .insert([{ 
        name: newComment.value.name.trim() || "Anonymous",
        comment: newComment.value.comment.trim(), 
        ...(storedEmail && { email: storedEmail }),
        created_at: new Date().toISOString()
      }])
      .select('*');

    if (!error && data.length > 0) {
      comments.value.unshift({ ...data[0], replies: [] });

      // ✅ Store the user's comment name for replies
      localStorage.setItem("commenter_name", newComment.value.name.trim());

      // ✅ Increment comment count
      localStorage.setItem("comment_count", (commentCount + 1).toString());

      // ✅ Set first comment time if this is the first one within 30 minutes
      if (commentCount === 0) {
        localStorage.setItem("first_comment_time", now.toString());
      }

      // ✅ Clear input fields
      newComment.value.name = '';
      newComment.value.comment = '';
    }
  } catch (error) {
    console.error("Error adding comment:", error);
  }
};

const toggleReplyForm = (commentId) => {
  replyForms.value[commentId] = !replyForms.value[commentId];
};

const hasUserCommented = computed(() => localStorage.getItem("comment_count") > 0);
const canUserReply = computed(() => hasUserCommented.value || userName.value);


const addReply = async (commentId) => {
  if (!newReply.value[commentId]?.trim()) return;

  // Get the stored commenter name or fallback to guestbook name
  const storedCommenterName = localStorage.getItem("commenter_name");
  const finalName = storedCommenterName || userName.value || "Anonymous";

  // Prevent reply if user is not in guestbook and hasn't commented
  if (!canUserReply.value) {
    alert("You must either have provided an email in the guestbook or have commented first before replying.");
    return;
  }

  try {
    let { data, error } = await supabase
      .from('replies')
      .insert([{ 
        name: finalName,  
        comment: newReply.value[commentId],
        parent_id: commentId,
        created_at: new Date().toISOString()
      }])
      .select('*');

    if (!error && data.length > 0) {
      comments.value = comments.value.map(comment =>
        comment.id === commentId ? { ...comment, replies: [...comment.replies, data[0]] } : comment
      );

      newReply.value[commentId] = '';
      replyForms.value[commentId] = false;
    }
  } catch (error) {
    console.error("Error adding reply:", error);
  }
};

    const formatTimestamp = (timestamp) => {
      return timestamp ? new Date(timestamp).toLocaleString() : "Unknown time";
    };
    onMounted(async () => {
  localStorage.removeItem("comment_count");  // Resets on refresh during development
  await fetchGuestbookName();
  await fetchComments();
});

    // Gallery Section
    const images = ref([
      { id: 1, src: 'https://github.com/rainvp/Personal-Profile-Webpage/blob/main/images/460961978_967543388415623_4541161538742405339_n.jpg?raw=true' },
      { id: 2, src: 'https://github.com/rainvp/Personal-Profile-Webpage/blob/main/images/472789858_1157284476015373_4532978188250656890_n.jpg?raw=true' },
      { id: 3, src: 'https://github.com/rainvp/Personal-Profile-Webpage/blob/main/images/472478541_1393676961599516_8296656406198264170_n.jpg?raw=true' },
      { id: 4, src: 'https://github.com/rainvp/Personal-Profile-Webpage/blob/main/images/363829702_970044974249532_9015369949003698015_n.jpg?raw=true' },
      { id: 5, src: 'https://raw.githubusercontent.com/rainvp/Personal-Profile-Webpage/refs/heads/main/images/4ebab79f-86d0-41ab-b557-e37c20843d4b.jfif' },
      { id: 6, src: 'https://github.com/rainvp/Personal-Profile-Webpage/blob/main/images/472699294_466149492989920_1496860658682248426_n.jpg?raw=true' },
      { id: 7, src: 'https://github.com/rainvp/Personal-Profile-Webpage/blob/main/images/8DD1B940-891E-44AA-BFCC-A3BE20992CDB.jpg?raw=true' },
      { id: 8, src: 'https://github.com/rainvp/Personal-Profile-Webpage/blob/main/images/af29de30-95ab-420c-90d6-6d6e91d783d3.jpg?raw=true' },
      { id: 9, src: 'https://github.com/rainvp/Personal-Profile-Webpage/blob/main/images/IMG_3543%20(2).JPG?raw=true' },
      { id: 10, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842153493467348/10.jpg?ex=67c9a800&is=67c85680&hm=d994e43d9aaac153694e19625e97667ef7d27da006927cf738e67d64bf19ebb5&' },
      { id: 11, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842176092639293/11.jpg?ex=67c9a805&is=67c85685&hm=f993f65c70b0f5c41c2c5fed450f2bec3b17382e0ed989ff59108bef69856dd9&' },
      { id: 12, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842200620793937/12.jpg?ex=67c9a80b&is=67c8568b&hm=f471cdd4a19881f00ae2328bd8e1afee70a3e344d4f549c2b56408168980bd85&' },
      { id: 13, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842218777939978/13.jpg?ex=67c9a810&is=67c85690&hm=db2cfa00b64608c545f1b9808bd791827f181598185ed8aeb5faa58c5b607408&' },
      { id: 14, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842252068130857/14.jpg?ex=67c9a818&is=67c85698&hm=ce9bb8e825b67e410634e94c9452f82382e48e6764fefd9b13f743bc05b61931&' },
      { id: 15, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842287157678142/15.jpg?ex=67c9a820&is=67c856a0&hm=bd46a3713b28f4b5c10a3b9b4449cd7cdc3178c21865f184e55472c98e353777&' },
      { id: 16, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842317298073620/16.jpg?ex=67c9a827&is=67c856a7&hm=92342fbe3b71a909c153fd69777bdab638efacfc4f32b6acff08791e477faade&' },
      { id: 17, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842317658787882/17.jpg?ex=67c9a827&is=67c856a7&hm=30c1ef03d8fb8144aa5f6393966d0023c3b8ae4dbc14c2dd3deaf74c3f3f613a&' },
      { id: 18, src: 'https://media.discordapp.net/attachments/1155238663953862718/1346842512505049108/18.jpg?ex=67c9a856&is=67c856d6&hm=eef46470d5d8280e79670327807ed6dc1e474faf790702ce72d9ccb20dedb7bb&=&format=webp&width=642&height=856' },
      { id: 19, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842513280860203/19.jpg?ex=67c9a856&is=67c856d6&hm=b982f797034c428e7474cd421ef6799f6bd2cec0b0fe11a5ff0ed7887c4b5dd2&' },
      { id: 20, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842513767530558/20.jpg?ex=67c9a856&is=67c856d6&hm=714f17e0f7758bda0f6ae122e92a1273b5019b8a3a1fc0bdb9660eab8c5d0064&' },
      { id: 21, src: 'https://cdn.discordapp.com/attachments/1155238663953862718/1346842514157604904/21.jpg?ex=67c9a856&is=67c856d6&hm=fb4b5329164db9301962f53268de7c6dab2ffc90700d0b477dc8d444a0b3c7e1&' },
    ]);

    const captions = ref([
    'Welcome to the gallery!🤎🥐',
    'Luv these photos <3 💌📸',
    'Proof I’m not friendless 🦢🎞️ (🤨🤨🤨)',
    'Got to see NIKI live!! (this is why I was born, my whole life has led up to this moment)🎀🎤',
    'Just another day in the archives. 🩰🍰',
    "Keychains, trinkets, and whatever else I collect for no reason (this is cheaper than therapy) 🔑💌",
    'Photobooths hate to see us coming.📸',
]);

    const currentIndex = ref(0);
    const itemsPerSlide = 3;

    const currentImages = computed(() => {
      const start = currentIndex.value * itemsPerSlide;
      return images.value.slice(start, start + itemsPerSlide);
    });

    const currentCaption = computed(() => captions.value[currentIndex.value] || '');

    const prevSlide = () => {
      currentIndex.value = (currentIndex.value === 0) 
        ? Math.floor(images.value.length / itemsPerSlide) 
        : currentIndex.value - 1;
    };

    const nextSlide = () => {
      currentIndex.value = ((currentIndex.value + 1) * itemsPerSlide >= images.value.length) 
        ? 0 
        : currentIndex.value + 1;
    };

    return {
      // Comments
      comments,
      newComment,
      addComment,
      replyForms,
      newReply,
      hasUserCommented,
      canUserReply,
      toggleReplyForm,
      addReply,
      formatTimestamp,
      userName,

      // Gallery
      images,
      captions,
      currentIndex,
      currentImages,
      currentCaption,
      prevSlide,
      nextSlide,
    };
  }
};

</script>

<style scoped>
body, html {
    height: 100%;
    font-family: 'Poppins', sans-serif;
    margin: 0;
    color: #4a3b2b;
    background-color: #fcf5e8;
}

 .menu {
    display: none;
 }

 a {
    text-decoration: none;
    color: inherit;
    transition: color 0.3s;
}

p {
   font-size: 18px;
}

.tag {
  width: 100%;
  font-size: 28px;
  font-weight: bold;
  color: #5a391f;
  margin-bottom: 2px;
  text-transform: uppercase;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 50px;
  margin-bottom: 50px;
  font-weight: bold;
  letter-spacing: 2px; /* Add some spacing between letters */
  position: relative; /* For positioning the lines */
}

.tag::before {
  content: "";
  flex: 1; 
  height: 3px; 
  flex-grow: 5; /* Makes the lines expand further */
  background: linear-gradient(to right, #d4b59b, #502917);
  margin: 0 15px;
}
.tag::after {
  content: "";
  flex: 1; 
  flex-grow: 5; /* Makes the lines expand further */
  height: 3px; 
  background: linear-gradient(to left, #d4b59b, #502917); /* Gradient effect */
  margin: 0 15px;
}


/*--------------------------------------------- Custom Styles------------------------------------------- */

/* ---------------------------------------- Navigation Bar ---------------------------------------------- */
.navbar {
    position: fixed;
    top: 0;
    width: 100%;
    background-color: #f7e7d1; 
    color: #4a3b2b;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px;
    z-index: 1000;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1); 
}

.navbar .logo img {
    height: 65px; /* Adjust the height of the logo */
    width: auto; /* Maintain aspect ratio */
    display: block; /* Ensure proper spacing around the image */
}


.navbar a {
    color: #4a3b2b; 
    font-size: 20px;
    text-decoration: none; 
    padding: 10px 25px; 
    transition: background-color 0.3s ease, color 0.3s ease; 
}

.navbar a:hover {
    background-color: #d4b59b; 
    color: #fff; 
    border-radius: 5px;
}

/* Dropdown styling */
.dropdown {
    position: relative;
    display: inline-block;
}

.dropbtn {
    background-color: transparent;
    border: none;
    cursor: pointer;
    font-size: 16px;
    color: #4a3b2b;
    padding: 10px 15px;
    transition: color 0.3s ease;

      /* Remove unwanted shadows */
  box-shadow: none;
  text-shadow: none;
}

.dropbtn:hover {
    color: #d4b59b;
}

/* Dropdown icon */
.dropdown-icon {
    font-size: 16px;
    margin-left: 5px;
    transition: transform 0.3s ease; /* Animation for rotation */
}

/* Dropdown content */
.dropdown-content {
    display: none;
    position: absolute;
    right: 0; /* Align dropdown below the icon */
    background-color: #fff;
    box-shadow: 0px 8px 16px rgba(0, 0, 0, 0.2);
    z-index: 1;
    min-width: 250px;
    border-radius: 5px;
    opacity: 0;
    visibility: hidden;
    transform: translateY(10px); /* Start with a slight downward position */
    transition: opacity 0.3s ease, visibility 0.3s ease, transform 0.3s ease; /* Smooth fade-in and slide-up */
}

/* Dropdown sections */
.dropdown-section {
    padding: 15px;
    border-bottom: 1px solid #f7e7d1;
}

.dropdown-title {
    font-size: 16px;
    font-weight: bold;
    color: #4a3b2b;
    margin-bottom: 10px;
    text-transform: uppercase; /* Optional: Make titles uppercase for a neat look */
}

/* Dropdown items */
.dropdown-content a {
    color: #4a3b2b;
    padding: 8px 15px;
    text-decoration: none;
    display: block;
    transition: background-color 0.3s ease;
}

.dropdown-content a:hover {
    background-color: #f7e7d1;
}

/* Show dropdown on hover */
.dropdown:hover .dropdown-content {
    display: block;
    opacity: 1;
    visibility: visible;
    transform: translateY(0); /* Slide to the original position */
}

/* Rotate the arrow when dropdown is open */
.dropdown:hover .dropdown-icon {
    transform: rotate(180deg); /* Rotate arrow */
}

/* Ensure dropdown works on mobile */
.dropdown:focus-within .dropdown-content,
.dropdown:hover .dropdown-content {
    display: block;
    opacity: 1;
    visibility: visible;
    transform: translateY(0); /* Slide to the original position */
}

@media screen and (max-width: 768px) {
  .navbar {
    display: flex;
    justify-content: center; /* Center items */
    align-items: center;
    padding: 10px;
    flex-wrap: wrap; /* Allow wrapping if needed */
  }

  .logo {
    display: none; /* Hides logo on mobile */
  }

  .nav-links {
    display: flex;
    flex-wrap: wrap;
    gap: 10px; /* More spacing for better touch accessibility */
    justify-content: center;
    align-items: center;
  }

  .nav-links a {
    font-size: 14px;
    padding: 10px 12px;
    text-align: center;
  }

  .dropbtn {
    display: flex;
    align-items: center;
  }

  .dropdown-icon {
    font-size: 14px;
    margin-left: 5px;
  }

  .dropdown-content {
    position: absolute;
    background: white;
    width: auto;
    min-width: 150px;
    text-align: left;
}

}


/* ------------------------------------------------ Banner & Header ---------------------------*/
#banner {
    height: 100vh;
    display: flex;
    justify-content: flex-start; 
    align-items: center; 
    padding-left: 90px;
    padding-top: 20px;  
    position: relative;
    overflow: hidden;
    background-position: center;
    background-size: cover;
    background-image: url("https://i.pinimg.com/originals/07/91/1f/07911f8ccbaa7f0462acd7ac534f020f.gif");
    min-height: 75%;
}

/* Optional Gradient Overlay for a softer look */
#banner:before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: linear-gradient(rgba(241, 179, 121, 0.39), rgba(255, 255, 255, 0.5));
}

/* Banner content section */
#banner-content {
    animation: fadeInLeft 1.5s ease-out;
    max-width: 50%; /* Restrict the content width */
    z-index: 2; /* Ensures content is above the background */
    position: relative;
    text-align: left;
}

/* Header styling */
#banner h1 {
    font-size: 5em;
    color:#fffaf5;
    margin-bottom: 15px;
    animation: fadeInLeft 1.5s ease-out;
    font-family: 'Poppins', sans-serif;
    letter-spacing: 2px; 
    font-weight: bold;
    line-height: 1.2;
}

/* Subheading styling */
#banner h2 {
    font-size: 1.8em;
    margin-bottom: 30px;
    animation: fadeInLeft 1.5s ease-out;
    font-style: italic;
    letter-spacing: 1px;
    font-family: 'Arial', sans-serif;
    line-height: 1.5;
}

/* Button styling */
#banner .button {
    background-color: #502917;
    color: #fff;
    margin-top: 15px;
    padding: 22px;
    text-decoration: none;
    border-radius: 30px;
    font-size: 20px;
    transition: background-color 0.3s, transform 0.3s;
    position: relative;
    display: inline-block; 
    text-align: center;
}

/* Add hover effect */
#banner .button:hover {
    background-color: #6a3d22;
    transform: scale(1.05); 
}

/* Responsive adjustments */
@media (max-width: 768px) {
    #banner .button {
        padding: 0.8em 1.5em; /* Adjust padding for smaller screens */
        font-size: 1rem; /* Adjust font size */
    }
}

@media (max-width: 480px) {
    #banner .button {
        padding: 0.6em 1em; /* Further adjust for very small screens */
        font-size: 0.9rem;
        margin: 0.5em;
    }
}

/* Fade-in left animation */
@keyframes fadeInLeft {
    0% {
        opacity: 0;
        transform: translateX(-50px);
    }
    100% {
        opacity: 1;
        transform: translateX(0);
    }
}

/* Centering and limiting gallery size */
.gallery-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  max-width: 1500px;
  margin: auto;
  padding: 10px;
}

/* Gallery slider layout */
.gallery-slider {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  width: 100%;
  max-width: 1200px;
  height: auto;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  background-color: #f7e7d1;
}

/* Image wrapper */
.slider-images-wrapper {
  display: flex;
  transition: transform 0.5s ease-in-out;
  width: 100%;
}

/* Individual image */
.slider-image {
  flex: 0 0 calc(100% / 3);
  max-width: calc(100% / 3);
  padding: 5px;
  box-sizing: border-box;
}

.gallery-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.slider-nav {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  font-size: 24px;  /* Adjust arrow size */
  color: white;
  background-color: rgba(0, 0, 0, 0.6);  /* Less opacity */
  border: none;
  border-radius: 50%;  /* Ensures it's circular */
  padding: 10px;  /* Adjust padding */
  cursor: pointer;
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
  width: 40px;  /* Fixed size */
  height: 40px;  /* Fixed size */

    /* Remove unwanted shadows */
  box-shadow: none;
  text-shadow: none;
}

.slider-nav:hover {
  background-color: rgba(0, 0, 0, 0.8);
}


.left-arrow {
  left: 15px;  /* Adjusted for equal spacing */
}

.right-arrow {
  right: 15px; /* Adjusted for equal spacing */
}


/* Caption styling */
.slider-caption {
  text-align: center;
  font-size: 14px;
  color: #551f18;
  font-family: "Inconsolata", sans-serif;
  margin-top: 10px;
}

/* Responsive Design */
@media (max-width: 1200px) {
  .gallery-slider {
    max-width: 900px;
  }
  .slider-image {
    flex: 0 0 calc(100% / 2);
    max-width: calc(100% / 2);
  }
}

@media (max-width: 768px) {
  .gallery-slider {
    max-width: 600px;
  }
  .slider-image {
    flex: 0 0 100%;
    max-width: 100%;
  }
  .slider-nav {
    font-size: 24px;
    padding: 6px 10px;
  }
}

@media (max-width: 480px) {
  .gallery-slider {
    max-width: 100%;
  }
  .slider-nav {
    font-size: 20px;
    padding: 5px 8px;
  }
}
  /* Comments Section */
  .comments-section {
    max-width: 1000px;
    width: 100%;
    margin: 2rem auto;
    margin-bottom: 85px;
    padding: 20px;
    background: #f4e4d7;
    font-family: cursive;
    border: 4px solid #c99f82;
    box-shadow: 8px 8px 0px #5e3d2b;
    text-align: center;
  }
  
  /* Title Styling */
  .comments-section h2 {
    font-size: 24px;
    color: #755049;
    margin-bottom: 1rem;
    font-weight: bold;
    font-family: 'Press Start 2P';
  }
  
  /* Comment Form */
  .comment-form {
    display: flex;
    flex-direction: column;
    gap: 12px;
    padding: 1.2rem;
  }
  
  .comment-form input,
  .comment-form textarea {
    width: 100%;
    padding: 12px;
    font-family: inherit;
    border: 2px solid #c98b72;
    border-radius: 3px;
    font-size: 1rem;
    background: #fffaf5;
    color: #4a3f35;
    box-shadow: 4px 4px 0px #5e3d2b;
  }
  

  .comment-form textarea {
    resize: none;
    min-height: 100px;
  }
  
  .comment-form button {
    padding: 12px;
    background: #c48d74;
    color: white;
    font-size: 12px;
    font-family: 'Press Start 2P';
    letter-spacing: 2px;
    border: none;
    text-transform: uppercase;
    border-radius: 3px;
    cursor: pointer;
    transition: 0.3s;
    cursor: pointer;
    font-weight: bold;
    transition: transform 0.1s;
    box-shadow: 4px 4px 0px #5e3d2b;
  }

/* Push-up effect */
.comment-form input:focus,
.comment-form textarea:focus {
  outline: none;
  transform: translateY(-3px);
  box-shadow: 2px 2px 0px #5e3d2b;
  margin-bottom: 16px; /* Slightly increases spacing below */
}

/* Adjust margin of the next sibling to push it back */
.comment-form input:focus + textarea,
.comment-form textarea:focus + button {
  margin-top: -8px;
}
/* Retro Button Click Effect */
.comment-form button:active {
  transform: translate(3px, 3px);
  box-shadow: 2px 2px 0px #5e3d2b;
}

  /* Comments List */
  .comments-list {
    margin-top: 1.5rem;
    display: flex;
    flex-direction: column;
    gap: 15px;
    padding: 0 10px;
  }

  .comments-list {
  margin-top: 1.5rem;
  display: flex;
  flex-direction: column;
  gap: 15px;
  padding: 0 10px;
  max-height: 400px;
  overflow-y: auto;
  scrollbar-width: thin; /* Firefox */
  scrollbar-color: #c99f82 #f4e4d7; /* Firefox */
}

/* WebKit Scrollbar */
.comments-list::-webkit-scrollbar {
  width: 8px;
}

.comments-list::-webkit-scrollbar-thumb {
  background: #c99f82;
  border-radius: 6px;
}

.comments-list::-webkit-scrollbar-track {
  background: #f4e4d7;
  border-radius: 6px;
}
  
  /* Comment Box */
  .comment-box {
    background: #ffeadd;
    padding: 14px;
    border-radius: 12px;
    box-shadow: 2px 3px 10px rgba(0, 0, 0, 0.08);
    text-align: left;
    border-left: 4px solid #d3a484;
    position: relative;
    transition: transform 0.2s ease-in-out, box-shadow 0.2s;
    display: flex;
    flex-direction: column;
    width: 100%;

    
  }
  
  .comment-box:hover {
    transform: translateY(-3px);
    box-shadow: 4px 5px 15px rgba(0, 0, 0, 0.12);
  }
  
  .comment-box p {
    font-size: 1rem;
    margin: 0;
  }
  
  .comment-box span {
    font-size: 0.85rem;
    color: #e08c8c;
    display: block;
    margin-top: 6px;
  }
  
/* Reply trigger (small text link) */
.reply-trigger {
  font-size: 0.99rem;
  color: #6d6159;
  cursor: pointer;
  text-decoration: none;
  margin-top: 2px;
  display: inline-block;
}

.reply-trigger:hover {
  color: #8c7463;
  text-decoration: underline;
}

/* Reply Form */
.reply-form {
  margin-top: 4px;
  display: flex;
  flex-direction: column;
  gap: 4px;
  background: transparent; /* No background box */
  padding: 0;
  border-left: none; /* Remove border */
}

.reply-form input {
  width: 100%;
  padding: 10px;
  font-size: 0.8rem;
  border: 1px solid #d4a98d;
  border-radius: 3px;
  background: #fffaf5;
  color: #5a4c43;
  font-family: inherit;
}

.reply-form button {
  padding: 6px;
  background: #c8a08b;
  color: white;
  font-size: 10px;
  border: none;
  border-radius: 3px;
  cursor: pointer;
  box-shadow: none;
  text-shadow: none;
  transition: background 0.2s, transform 0.1s;
  align-self: flex-start; /* Align button to left */
}

.reply-form button:hover {
  background: #b98f7b;
}

.reply-form button:active {
  transform: translateY(1px);
}

/* Replies List */
.replies-list {
  margin-top: 4px;
  padding-left: 10px;
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.reply-box {
  background: transparent;
  padding: 4px;
  font-size: 0.8rem;
}

.reply-box p {
  margin: 0;
}

.reply-box span {
  font-size: 0.7rem;
  color: #a28b7c;
  display: block;
  margin-top: 2px;
}

</style>