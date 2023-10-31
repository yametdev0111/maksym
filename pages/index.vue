<template>
  <div class="landing-container">
    <!-- Header -->
    <section class="section landing">
      <div class="container">
        <header class="landing__header">
          <h1 class="landing__header-text">
            <span class="landing__name">I'm Maksym<span class="text--orange">.</span></span>
            <br> 
            <div class="landing__subheader text--blue">{{ this.jobTitle }}</div>
          </h1>
          <a class="landing__link" href="/contact"><button class="landing__btn btn--orange btn--outline">Contact Me!</button></a>
        </header>
      </div>
      <video class="landing__canvas" id="landingCanvas" src="https://hugo.fyi/res/video/hero1/hero1.mp4" autoplay />
      <!-- <video class="landing__canvas" id="landingCanvas" src="~/assets/videos/hero1.mp4" autoplay /> -->
    </section>
    <!-- Header End -->

    <!-- Portfolio Section -->
    <section class="section landing-portfolio">
      <div class="container">
        <div class="landing-portfolio__header">
          <SectionBody class="section__header" title="My Portfolio">
            <p>Here's a few highlights from projects I've worked on over the years. Interested in seeing more? Check out <a class="section__work-link" href='/work'>my work</a> page.</p>
          </SectionBody>
          
          <a href="/work" class="landing-portfolio__work-btn btn--orange btn--outline">See more</a>
        </div>

        <PortfolioPlanet 
          :planet="true" 
          :skills="['C++', 'AAA', 'Ubisoft', 'UE4']"
          title="Avatar Frontiers of Pandora"
          desc="Avatar: Frontiers of Pandora™ is a first person, action-adventure game developed by Massive Entertainment – a Ubisoft studio, in collaboration with Lightstorm Entertainment and Disney. Built using the latest iteration of the Snowdrop engine, and developed exclusively for the new generation of consoles and PC, Avatar: Frontiers of Pandora brings to life the alluring world of Pandora with all of its beauty and danger in an immersive, open world experience. In this new, standalone story, play as a Na’vi and embark on a journey across the Western Frontier, a never-before-seen part of Pandora. Explore a living and reactive world inhabited by unique creatures and new characters, and push back the formidable RDA forces that threaten it."
          imgSrc="http://hugo.fyi/assets/projectThumbs/fop-thumb3.png"
          gitLink="https://github.com/iEnder/Course-Tracker-Mobile"
        />

        <PortfolioPlanet 
          :planet="true"
          :skills="['UE4', 'C++', 'Gamedev', 'University']"
          title="Bolt Storm"
          desc="Bolt Storm features both ranged (gun, crossbow) and melee (sword, knife) combat. To allow for these different types of weapons, I set up a system which can map bones ('sockets') of characters to a specific slot, so that weapons can be used on different skeletons. The slot definitions, weapons themselves, and even the local binding have local offsets, to fine-tune the position in every case."
          imgSrc="http://hugo.fyi/assets/projectThumbs/BoltStorm-thumb-new.jpg"
          gitLink="https://github.com/iEnder/Discord5eArmory"
        />

        <PortfolioPlanet 
          :planet="true"
          :skills="['UE4', 'C++', 'Gamedev', 'University']"
          title="Soul Knight" 
          desc="In the video there are two circles, a bigger and smaller one. The bigger one (and all its properties) is used while the player is running, the smaller one is used while the player is walking. The camera system blends between them, based on the speed of the player. This allows the camera to be more precise and close-by while walking, and gives more of an overview while running. The circles can also grow / shrink and change properties dynamically, based on the scene for example, allowing shots which still keep the player in focus correctly while also adhering to the context of the scene."
          imgSrc="http://hugo.fyi/assets/projectThumbs/thumbSoulKnight.png"
          gitLink="https://github.com/iEnder/bb-leaderboards"
        />
      </div>
    </section>
    <!-- Portfolio Section End -->

    <!-- About Section -->
    <section class="section landing-about">
      <div class="container">
        <AboutSection class="section__header" />  
      </div>
    </section>
    <!-- About Section End -->

    <!-- Contact Section -->
    <section class="section landing-contact">
      <div class="container">
        <SectionBody class="section__header" title="Contact Me">
          <p>If you're looking to collaborate on a project, get in touch about a position, or say hi, feel free to use the form below. I'll be in touch with you as soon as I can.</p>
        </SectionBody>

        <ContactForm class="landing-contact__form" />
      </div>
    </section>
    <!-- Contact Section  End -->

    <!-- Footer -->
    <footer class="footer">
      <p>Designed and Developed By Maksym Hulhevych</p>
    </footer>
    <!-- Footer End -->
  </div>
</template>

<script>
import * as THREE from 'three';

export default {
  name: 'IndexPage',
  methods: {
    // Page Functions
    updateMouse() {
      const mouseEl = document.querySelector('#mouseEl');
      document.addEventListener('mousemove', onDocumentMouseMove, false);

      function onDocumentMouseMove(event) {
          event.preventDefault();
          mouseEl.style.left = `${event.pageX}px`;
          mouseEl.style.top = `${event.pageY}px`;
      }
    },
    
    animateJobTitle() {
      const index = Math.floor(Math.random() * this.titleList.length - 1);

      // get title from list but dont include already selected title
      let selectedTitle = this.titleList.filter(el => el !== this.jobTitle)[index].split('');

      // set title to first character to keep up content spacing
      this.jobTitle = selectedTitle.shift();

      for(let i = 1; i < selectedTitle.length + 1; i++) {
        let interval = 50 * i;
        setTimeout(() => {
          this.jobTitle += selectedTitle.shift();
        }, interval);
      }

    }
  },
  mounted: function() {
    let jobTitalInterval = setInterval(() => {
      this.animateJobTitle()
    }, 5000)
  },
  data() {
    return {
      jobTitle: 'Full Stack Game Developer',
      titleList: ['Unity Developer', 'UE4 Developer', '2D/3D Graphic Game Developer', 'Front-End Developer', 'Back-End Developer', 'Full-Stack Developer']
    }
  },
  head() {
    return {
      title: `Maksym Hulhevych | ${ this.jobTitle }`,
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Hey There! I\'m a Creative Software Developer with a passion for designing and building applications. Looking to collab? Check out my portfolio and get in touch.'
        }
      ],
    }
  }
}
</script>

<style lang="scss" scoped>
  @import '~/assets/css/landing';
</style>