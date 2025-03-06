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
                  <h1>Steamed & Skilled</h1>
              </div>
          </div>
      </div>
  </header>

<div class="resume-container" data-aos="fade-up">
  <h5 class="tag">From Books to Bytes</h5>
  <div class="card" data-aos="fade-up">
      <i class="fas fa-university school-icon"></i>
      <div class="school-name">Asia Pacific College</div>
      <div class="year">2023-2027 (Ongoing)</div>
      <div class="honors">Honour Student (1st Year)</div>
      <div class="role">Secretariat Officer at Junior Information Systems Security Association</div>
  </div>

  <div class="card" data-aos="fade-up">
      <i class="fas fa-school school-icon"></i>
      <div class="school-name">AMA University</div>
      <div class="year">2022-2023</div>
      <div class="honors">Grade 12 (With High Honours)</div>
  </div>

  <div class="card" data-aos="fade-up">
      <i class="fas fa-graduation-cap school-icon"></i>
      <div class="school-name">FEU High School</div>
      <div class="year">2021-2022</div>
      <div class="honors">Grade 11 (With Honours)</div>
      <div class="role">Member of the Association of Young Accountants</div>
  </div>

  <div class="card" data-aos="fade-up">
      <i class="fas fa-users school-icon"></i>
      <div class="school-name">Starland International School</div>
      <div class="year">2018-2021</div>
      <div class="honors">Grade 8-10 (With High Honours)</div>
      <div class="role">Grade 10 Student Learners' Council President (VisMin Branch)</div>
  </div>

  <div class="card" data-aos="fade-up">
      <i class="fas fa-book school-icon"></i>
      <div class="school-name">Asian Learning Center</div>
      <div class="year">2017-2018</div>
      <div class="honors">Grade 7 (With High Honours)</div>
  </div>
</div>

<section class="skills-section">
    <h5 class="tag" data-aos="fade-up">Barista's Tools</h5>

    <div class="teapot-container" data-aos="fade-up">
      <div class="teapot" :class="{ tilt: isPouring }"></div>
      <div class="liquid" :class="{ pouring: isPouring }"></div>
    </div>

    <button class="pour-button" data-aos="fade-up" @click="restartAnimation">Click Me!</button>

    <div class="progress-wrapper" data-aos="fade-up">
      <div v-for="(skill, index) in skills" :key="index" class="skill-item">
        <div class="skill-category">{{ skill.category }}</div>
        <div class="progress-container">
          <div 
            class="progress-bar" 
            :style="{ width: skill.progress + '%' }"
          ></div>
          <span class="progress-text">{{ skill.progress }}%</span>
        </div>
      </div>
    </div>
  </section>

  <section class="profile-showcase" data-aos="fade-up">
  <h2 class="tag">Skillfolio ☕✨</h2>

  <div class="showcase-card">
  <div class="showcase-card-title">Leadership & Team Collaboration</div>
  <div class="showcase-card-content">
    <ul>
      <li>🔹 <strong>UI/UX Prototyping Lead</strong> – Co-led a team in designing an interactive Figma prototype, ensuring a seamless user experience with intuitive design principles.</li>
    </ul>
  </div>
</div>

<div class="showcase-card">
  <div class="showcase-card-title">Programming, Development, & Problem-Solving</div>
  <div class="showcase-card-content">
    <ul>
      <li>🔹 <strong>Financial Transaction Simulation</strong> – Developed a custom tool for managing deposits, withdrawals, and transfers, improving efficiency and record-keeping.</li>
    </ul>
  </div>
</div>

<div class="showcase-card">
  <div class="showcase-card-title">Content Creation & Digital Presence</div>
  <div class="showcase-card-content">
    <ul>
      <li>🔹 <strong>Client Content Creation</strong> – Produced engaging digital content to establish brand identity, enhancing audience engagement and online reach.</li>
      <li>🔹 <strong>Personal Content Creation</strong> – Growing as a beauty and makeup content creator on TikTok, experimenting with creative strategies to connect with audiences.</li>
    </ul>
  </div>
</div>

<div class="showcase-card">
  <div class="showcase-card-title">Academic & Educational Support</div>
  <div class="showcase-card-content">
    <ul>
      <li>🔹 <strong>Academic Writing & Tutoring</strong> – Skilled in structuring well-researched academic papers for high school and elementary levels. Also provides tutoring, especially in mathematics.</li>
    </ul>
  </div>
</div>

<div class="showcase-card">
  <div class="showcase-card-title">Administrative & Organizational Skills</div>
  <div class="showcase-card-content">
    <ul>
      <li>🔹 <strong>Administrative Support</strong> – Experienced in data entry, file organization, and calendar management to maintain efficient workflows.</li>
    </ul>
  </div>
</div>
</section>


</template>

<script>
export default {
  data() {
    return {
      isPouring: false,
      skills: [
        { category: "Programming (Python, JavaScript)", progress: 0, target: 80 },
        { category: "Web Development (HTML, CSS, Vue.js)", progress: 0, target: 75 },
        { category: "Development Tools (VS Code, GitHub, Vercel)", progress: 0, target: 70 },
        { category: "Databases (MySQL, Supabase, PostgreSQL, XAMPP)", progress: 0, target: 60 },
        { category: "UI/UX & Graphic Design (Canva, Figma)", progress: 0, target: 90 },
        { category: "Productivity Tools (Office 365, Google Suite)", progress: 0, target: 95 }
      ]
    };
  },
  methods: {
    restartAnimation() {
      this.isPouring = false;
      this.skills.forEach(skill => skill.progress = 0);

      setTimeout(() => {
        this.isPouring = true;
        this.fillProgressBars();
      }, 200);
    },

    fillProgressBars() {
      this.skills.forEach((skill, index) => {
        let progress = 0;
        const interval = setInterval(() => {
          if (progress < skill.target) {
            this.skills[index].progress = ++progress;
          } else {
            clearInterval(interval);
          }
        }, 20);
      });
    }
  }
}
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
    background-image: url("https://github.com/rainvp/Personal-Profile-Webpage/blob/feature/4_rvp_finalswebsite/images/banner2.jpg?raw=true");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 20% 60%;
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
.resume-section {
    width: 100%;
    margin-bottom: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
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
  margin-top: 15px;
  margin-bottom: 25px;
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
/* Container with centered cards */
.resume-container {
    max-width: 1000px;
    margin: auto;
    padding: 40px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 40px;
}

/* Individual School Card */
.card {
    background: #ffffff;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    height: 260px;
    width: 280px;
    text-align: center;
    display: flex;
    flex-direction: column;
    align-items: center;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.card:hover {
    transform: translateY(-5px);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15);
    background: #faecd2;
}

/* School Icon */
.school-icon {
    font-size: 50px;
    color: #5a391f;
    margin-bottom: 10px;
}

/* School Name */
.school-name {
    font-weight: bold;
    font-size: 1.2rem;
    color: #5a391f;
}

/* Year Styling */
.year {
    font-style: italic;
    color: #666;
    margin-bottom: 10px;
}

/* Honors & Roles */
.honors {
    font-weight: bold;
    color: #5a391f;
}

.role {
    font-size: 0.9rem;
    color: #444;
}

ul {
    list-style-type: none;
    padding: 0;
}
li {
    font-size: 1.2rem;
    padding: 5px 0;
}

.skills-section {
    max-width: 1300px;
    margin: auto;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px;
  }
  
  .teapot-container {
    position: relative;
    width: 100px;
    height: 100px;
    margin-bottom: 20px;
  }
  .teapot {
    width: 100%;
    height: 100%;
    background: url('https://media.discordapp.net/attachments/1155238663953862718/1346810061263212576/teapot.png?ex=67c98a1d&is=67c8389d&hm=a3be564c230d46ef55b67b0bc36dffc71b0e8d1d83a6b15d55d32f988bbc3efa&=&format=webp&quality=lossless') no-repeat center;
    background-size: contain;
    transform-origin: top center;
    transition: transform 0.5s ease;
  }
  .teapot.tilt {
    transform: rotate(48deg);
  }
  .liquid {
    position: absolute;
    top: 80px;
    left: 50%;
    width: 8px;
    height: 0;
    background-color: #806d5a;
    transform: translateX(-50%);
    transition: height 0.5s ease;
    z-index: -1;
  }
  .liquid.pouring {
    height: 80px;
  }
  
  .pour-button {
  background-color: #614f41;
  color: white;
  border: none;
  padding: 10px 10px;
  cursor: pointer;
  font-size: 16px;
  border-radius: 5px;
  margin-bottom: 20px;
  transition: background 0.3s;
  
  /* Prevents button from being too long */
  max-width: 200px;  /* Adjust as needed */
  width: fit-content;
  display: block;  /* Prevents it from stretching */
    /* Remove unwanted shadows */
  box-shadow: none;
  text-shadow: none;
}

.pour-button:hover {
  background-color: #91765f; /* Darker shade for hover effect */
 
}

  .progress-wrapper {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
    max-width: 1200px;
  }
  
  .skill-item {
    width: calc(50% - 10px);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }
  
  .skill-category {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 5px;
    color: #4b382a;
  }
  
  .progress-container {
    position: relative;
    width: 100%;
    height: 30px;
    background: rgb(192, 176, 159);
    border-radius: 5px;
    overflow: hidden;
    margin-right: 20px;
  }
  
  .progress-bar {
    position: absolute;
    left: 0;
    bottom: 0;
    height: 100%;
    background: linear-gradient(45deg, #68524c, #4b382a);
    transition: width 1s ease-in-out;
  }
  
  .progress-text {
    position: absolute;
    margin-top: 5px;
    z-index: 1;
    font-size: 14px;
    font-weight: bold;
    color: white;
    pointer-events: none;
    left: 50%;
    transform: translateX(-50%);
  }

/* Profile Showcase Container */
.profile-showcase {
  max-width: 1300px; /* Increased width */
  margin: 40px auto;
  padding: 20px;
  text-align: center;
}

/* Individual Cards */
.showcase-card {
  display: flex;
  flex-direction: column; /* Stack elements */
  border: 2px solid #d1bfa7;
  border-radius: 10px;
  padding: 20px;
  margin: 15px auto;
  background: #fff;
  box-shadow: 2px 4px 10px rgba(0, 0, 0, 0.1);
  text-align: left;
  max-width: 90%; /* Adjust width to fit larger screens */
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

/* Card Title */
.showcase-card-title {
  font-size: 20px;
  font-weight: bold;
  color: #5a391f;
  margin-bottom: 5px; /* Adjust spacing */
}

/* Card Content */
.showcase-card-content {
  text-align: justify;
  color: #333;
  font-size: 1rem;
}

/* Bullet Points */
.showcase-card-content ul {
  list-style: none;
  padding: 0;
}

.showcase-card-content li {
  font-size: 18px;
  margin-bottom: 8px;
  line-height: 1.5;
}

/* Hover Effect */
.showcase-card:hover {
  transform: translateY(-5px);
  box-shadow: 4px 8px 15px rgba(0, 0, 0, 0.15);
}

/* Responsive Design */
@media (max-width: 768px) {
  .showcase-card {
    max-width: 100%;
  }

  .showcase-card-title {
    font-size: 1.2rem;
  }

  .showcase-card-subtext {
    font-size: 0.9rem;
  }
}

  /* ------------------------------ footer ------------------------------*/
/* Full-Width Footer */
.footer {
  width: 100%; /* Ensures the footer spans the full width */
  background-color: #4a3b2b; /* Matching theme color */
  color: #fff;
  text-align: center;
  padding: 15px 20px;
  position: relative; /* Avoids unintended shifts */
}


.footer-content {
  margin: 0 auto; /* Centers the content */
  padding: 0 20px; /* Adds padding to prevent text from touching edges */
  display: flex;
  justify-content: space-between;
  align-items: center;
}


/* Footer Links */
.footer a {
  color: #f7e7d1;
  text-decoration: none;
  margin: 0 10px;
  font-size: 16px;
}

.footer a:hover {
  color: #d4b59b; /* Slight hover effect */
}

/* Social Media Icons */
.footer .social-icons {
  display: flex;
  gap: 15px;
}

.footer .social-icons a {
  font-size: 20px;
}

/* Responsive Footer */
@media (max-width: 600px) {

  /* Full-Width Footer */
  .footer {
  width: 100%; /* Ensures the footer spans the full width */
  background-color: #4a3b2b; /* Matching theme color */
  color: #fff;
  text-align: center;
  padding: 10px 10px;
  position: relative; /* Avoids unintended shifts */
}

.footer-content {
  margin: 0 auto; /* Centers the content */
  padding: 10px 10px; /* Adds padding to prevent text from touching edges */
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
  text-align: center;
  gap: 10px;
  
}

}
</style>
