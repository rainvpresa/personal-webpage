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

  <!-- Banner Section -->
  <header id="banner">
      <div id="banner-content" class="row clearfix">
          <div class="col-38">
              <div class="section-heading">
                  <h1>Poured Over Pages</h1>
              </div>
          </div>
      </div>
  </header>

  <div class="resources-container">
    <h1 class="tag">Website Development Resources</h1>
    
    <div v-for="(category, index) in resources" :key="index" class="resource-card">
      <h2 class="resource-title">{{ category.title }}</h2>
      <ul class="resource-list">
        <li v-for="(item, i) in category.items" :key="i">
          <strong>
            <a v-if="item.link" :href="item.link" target="_blank" rel="noopener noreferrer">
              {{ item.name }}
            </a>
            <span v-else>{{ item.name }}</span>
          </strong>
          – {{ item.description }}
        </li>
      </ul>
    </div>
  </div>


</template>

<script>
export default {
  data() {
    return {
      resources: [
        {
          title: "Hosting & Deployment",
          items: [
            { name: "GitHub", description: "Version control and repository hosting", link: "https://github.com/" },
            { name: "Vercel", description: "Frontend deployment", link: "https://vercel.com/" },
            { name: "PythonAnywhere", description: "Flask backend hosting", link: "https://www.pythonanywhere.com/" },
          ],
        },
        {
          title: "Visual & Design Elements",
          items: [
            { name: "Personal Photos", description: "Used for images on the website" },
            { name: "Canva", description: "Logo design", link: "https://www.canva.com/" },
            { name: "Pinterest", description: "Source of GIFs", link: "https://www.pinterest.com/" },
            { name: "Google Fonts", description: "Typography selection", link: "https://fonts.google.com/" },
            { name: "FontAwesome", description: "Icons for UI elements", link: "https://fontawesome.com/" },
          ],
        },
        {
          title: "Development & Learning Resources",
          items: [
            { name: "W3Schools", description: "Reference for HTML, CSS, and JavaScript", link: "https://www.w3schools.com/" },
            { name: "Slider Revolution", description: "JavaScript animation inspiration", link: "https://www.sliderrevolution.com/design/cool-javascript-animations/" },
            { name: "AOS Library", description: "Animations for scrolling effects", link: "https://michalsnik.github.io/aos/" },
          ],
        },
        {
          title: "Frontend Framework",
          items: [
            { name: "Vue.js", description: "Used for building interactive user interfaces", link: "https://vuejs.org/" },
          ],
        },
        {
          title: "Package Management & Dependencies",
          items: [
            { name: "npm", description: "Used for managing project dependencies", link: "https://www.npmjs.com/" },
            { name: "Node.js Modules", description: "Essential packages stored in `node_modules`", link: "https://nodejs.org/" },
          ],
        },
        {
          title: "Backend & Functionality",
          items: [
            { name: "Supabase", description: "Backend database and authentication", link: "https://supabase.com/" },
            { name: "Flask App", description: "Backend logic and API handling", link: "https://flask.palletsprojects.com/" },
          ],
        },
        {
          title: "AI Assistance & Debugging",
          items: [
            { name: "ChatGPT", description: "Code building, enhancement, and debugging", link: "https://openai.com/chatgpt" },
          ],
        },
      ],
    };
  },
};
</script>

<style scoped>
body, html {
    height: 100%;
    font-family: 'Poppins';
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
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
    margin-bottom: 60px; /* Spacing above and below the tag */
    font-size: 1.5rem; /* Adjust text size */
    font-weight: bold;
    color: #4a3b2b; /* Coffee-inspired color */
    text-transform: uppercase; /* Make the text all caps */
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


#banner {
    height: 100vh;
    display: flex;
    justify-content: flex-start;
    align-items: center;
    padding-left: 90px;
    padding-top: 20px;
    position: relative;
    overflow: hidden;
    
    /* Background Image */
    background-image: url("https://i.pinimg.com/originals/ff/cc/14/ffcc142948cb780c24c5e5086fd57016.gif");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 20% 60%;
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

    /* Remove unwanted shadows */
  box-shadow: none;
  text-shadow: none;
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

.resources-container {
  max-width: 1200px;
  margin: 20px auto;
  padding: 20px;
  text-align: center;
}

.page-title {
  font-size: 28px;
  font-weight: bold;
  color: #5a391f;
  margin-bottom: 20px;
}

.resource-card {
  background: #fff;
  border: 2px solid #d1bfa7;
  border-radius: 12px;
  padding: 20px;
  margin-bottom: 20px;
  box-shadow: 3px 5px 12px rgba(0, 0, 0, 0.1);
  text-align: left;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.resource-title {
  font-size: 22px;
  font-weight: bold;
  color: #5a391f;
  margin-bottom: 10px;
}

.resource-list {
  list-style: none;
  padding: 0;
}

.resource-list li {
  font-size: 16px;
  margin-bottom: 8px;
  line-height: 1.6;
}

.resource-list a {
  color: #5a391f;
  text-decoration: none;
  font-weight: bold;
}

.resource-list a:hover {
  text-decoration: underline;
  color: #8a5a3f;
}

@media (max-width: 768px) {
  .resources-container {
    padding: 10px;
  }

  .resource-card {
    padding: 15px;
  }

  .page-title {
    font-size: 24px;
  }

  .resource-title {
    font-size: 20px;
  }

  .resource-list li {
    font-size: 14px;
  }
}
</style>
