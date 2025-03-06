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
                  <h1>Talk Over Tea</h1>
              </div>
          </div>
      </div>
  </header>

  <br>
  <br>
  <div class="contact-container">
    <img src="https://i.pinimg.com/originals/99/35/48/99354834273738b01a92ea362d77f347.gif" alt="Warm greeting GIF" class="contact-gif" />
    
    <h2 class="contact-title">Let's Stay Connected!☕</h2>
    
    <div class="contact-message">
      <p>Hey there! Just like a good cup of coffee, great conversations warm the soul.☕🍪
      Whether you want to chat, collaborate, or simply say hello, I'd love to hear from you!
      Feel free to reach out through any of the links below. Let's make something amazing together!🧇🥞🥖</p>
    </div>
    
    <div class="contact-links">
      <p>You can find me here:</p>
      <a href="mailto:rainvpresa@gmail.com" title="Email"><i class="fas fa-envelope"></i></a>
      <a href="https://www.instagram.com/iamrainvp" target="_blank" title="Instagram"><i class="fab fa-instagram"></i></a>
      <a href="https://www.linkedin.com/in/rain-cel-anne-sophia-presa-a428b7289/" target="_blank" title="LinkedIn"><i class="fab fa-linkedin"></i></a>
    </div>
  </div>

</template>

<script>
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
    background-image: url("https://i.pinimg.com/originals/ea/84/09/ea840917053aaea098f02fc1e60a7c13.gif");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 20% 5%;
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

/*---------------------------------- Contact-----------------------*/

.contact-container {
    max-width: 1250px;
    width: 100%;
    margin: 2rem auto 85px;
    padding: 20px;
    background: #ffe4cd;
    font-family: 'Poppins', sans-serif;
    border: 4px solid #c99f82;
    box-shadow: 8px 8px 0px #5e3d2b;
    text-align: center;
}

.contact-gif {
    width: 300px; /* Adjust width */
    height: auto; /* Maintain aspect ratio */
    margin-bottom: 15px; /* Adjust spacing */
    border-radius: 6px; /* Keep smooth edges */
}


.contact-title {
  margin: 30px;
    font-size: 28px;
    color: #5a3826;
    font-weight: bold;
    font-family: 'Press Start 2P', cursive;
}

.contact-message {
  background: #fff8dc; /* Warm background */
  padding: 10px 30px;
  margin: 5px 150px;
  border: 3px solid #8b5e3c; /* Brown border */
  box-shadow: 4px 4px 0px #5e3d2b; /* Vintage-style shadow */
  font-size: 16px; 
  font-family: cursive;
  position: relative;
  display: flex;
  flex-direction: column; /* Stack content vertically */
  gap: 5px; /* Space between elements */
  text-align: justify;
    
}

.contact-links a {
    display: inline-block;
    margin: 0 12px;
    font-size: 26px;
    color: #7d5c43;
    transition: color 0.3s, transform 0.2s;
    font-family: 'Press Start 2P', cursive;
}

.contact-links a:hover {
    color: #5a3826;
    transform: scale(1.1);
}

.contact-links p {
  font-size: 18px; 
  font-family: cursive;
  position: relative;
  display: flex;
  flex-direction: column; /* Stack content vertically */
  gap: 8px; /* Space between elements */
  text-align: center;
}

/*---------------------------------- Mobile Responsive Styles-----------------------*/
@media screen and (max-width: 768px) {
    .contact-container {
        width: 95%; /* Take up more space on mobile */
        margin: 1.5rem auto;
        padding: 15px;
    }

    .contact-title {
        font-size: 20px; /* Adjust title size */
        margin: 15px;
    }

    .contact-gif {
        width: 200px; /* Make it smaller for small screens */
    }

    .contact-message {
        font-size: 14px; /* Reduce text size */
        padding: 10px;
        margin: 5px auto;
        max-width: 90%;
    }

    .contact-links a {
        font-size: 18px; /* Adjust icons to fit */
        margin: 5px;
    }

    .contact-links p {
        font-size: 14px;
    }
}

</style>