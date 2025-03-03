<template>
  <div class="min-h-screen bg-gradient-to-b font-fugaz from-[#EFBF04] to-black flex flex-col items-center justify-center text-black relative">
    <div class="fixed top-5 right-5 z-20">
      <button @click="toggleMenu" class="bg-slate-800 text-white px-4 py-2 rounded-full hover:bg-gray-600">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
          <path stroke-linecap="round" stroke-linejoin="round" d="M3.75 6.75h16.5M3.75 12h16.5m-16.5 5.25h16.5" />
        </svg>

      </button>
      <div v-if="menuOpen" class="mt-2 bg-white shadow-lg rounded-lg p-4">
        <nav class="flex flex-col space-y-2">
          <a href="#features" @click="closeMenu" class="hover:text-yellow-600">Welcome</a>
          <a href="#about" @click="closeMenu" class="hover:text-yellow-600">About</a>
          <a href="#contact" @click="closeMenu" class="hover:text-yellow-600">Contact</a>
        </nav>
      </div>
    </div>

    <main class="w-full">
      <section id="features" class="h-screen flex items-center justify-center text-center opacity-0 translate-y-10 transition-all duration-700 ease-out relative overflow-hidden">
        <div class="drop-shadow-lg">
          <h3 class="text-5xl sm:text-7xl font-bold mb-4 relative">
            Die<span class="text-7xl sm:text-9xl" id="g-clef">𝄞</span>ounderia
          </h3>
          <p class="text-base sm:text-lg">Let the music guide your creativity and inspiration.</p>
        </div>
        <div class="absolute inset-0 pointer-events-none">
          <div v-for="(note, index) in musicalNotes" :key="index" :style="note.style" class="note">
            {{ note.symbol }}
          </div>
        </div>
      </section>

      <section id="about" class="h-screen drop-shadow-lg flex flex-col items-center justify-center text-center opacity-0 translate-y-10 transition-all duration-700 ease-out">
        <div class="w-full h-full max-w-6xl flex flex-col items-center justify-center">
          <h3 class="text-5xl sm:text-7xl drop-shadow-md text-[#E0E0E0] font-bold mb-8">What's on the Menu</h3>
          <div class="flex justify-center space-x-4 mb-8">
            <button @click="toggleSongs('personalized')" class="px-6 py-3 rounded-full" :class="{ 'bg-black text-white': selectedType === 'personalized', 'bg-gray-500 text-black hover:bg-[#E0E0E0] opacity-70': selectedType !== 'personalized' }">Personalized Menu</button>
            <button @click="toggleSongs('business')" class="px-6 py-3 rounded-full" :class="{ 'bg-black text-white': selectedType === 'business', 'bg-gray-500 text-black hover:bg-[#E0E0E0] opacity-70': selectedType !== 'business' }">Business Menu</button>
          </div>
          <div class="song-menu-container w-full h-[70vh] max-w-5xl grid gap-6 grid-cols-3 auto-rows-fr">
            <div v-for="(song, index) in personalizedSongs" :key="song.title" 
                :style="{ backgroundColor: song.color }" 
                class="song-card p-6 rounded-2xl shadow-lg hover:scale-105 transition-transform flex flex-col justify-between">
              <div>
                <h3 class="text-xl font-bold mb-2">{{ song.title }}</h3>
                <p class="text-sm mb-4">{{ song.description }}</p>
              </div>
              <button @click="playMusic(song.musicSrc)" class="play-button bg-white text-black py-2 px-4 rounded-full mt-auto">Play</button>
            </div>
          </div>
        </div>
        <div class="absolute flex items-center bottom-4 right-4 z-20">
          <button @click="togglePause" class="mr-4 px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition duration-300">
            {{ isPlaying ? 'Pause' : 'Resume' }}
          </button>
          <div class="space-x-2 bg-white bg-opacity-75 rounded-full p-2">
            <input type="range" id="volume" min="0" max="1" step="0.1" v-model="volume" class="w-full volume-slider" @input="setVolume" :style="sliderStyle" />
          </div>
        </div>
      </section>
      <section id="video" class="h-screen flex flex-col items-center justify-center text-center opacity-0 translate-y-10 transition-all duration-700 ease-out" ref="video">
        <p class="text-teal-600 text-xl sm:text-2xl mb-10">All music is royalty-free and available with exclusive rights upon request</p>
          <p class="text-sky-700 text-xl sm:text-2xl mb-8">Languages we personalize songs in: 
          <span class="text-sky-700 text-xl sm:text-2xl ">🇩🇪 German | 🇺🇸 English | Mundoat (Austrian dialect – our specialty!)</span>
          </p>
        <div class="flex flex-col items-center space-y-4 w-full max-w-4xl mx-auto">
          <video
            ref="video"
            src="/videos/bday.mp4"
            class="w-full rounded-lg shadow-lg"
            preload="auto"
            controls
          ></video>
        </div>
        <p class="text-pink-600 text-xl sm:text-2xl mt-8">Instrumental versions are also available. Videos & animations upon request.</p>
      </section>

      <section id="contact" class="h-screen text-white flex flex-col items-center justify-center text-center opacity-0 translate-y-10 transition-all duration-700 ease-out">
        <div class="drop-shadow-lg">
          <h3 class="text-4xl sm:text-5xl font-bold mb-4">Contact Us</h3>
          <p class="text-base sm:text-lg">Reach out to us for collaborations and inquiries.</p>
          <form @submit.prevent="submitForm" class="flex flex-col space-y-4 mt-8">
            <input v-model="contactForm.name" type="text" placeholder="Your Name" class="p-3 rounded-lg text-black" required />
            <input v-model="contactForm.email" type="email" placeholder="Your Email" class="p-3 rounded-lg text-black" required />
            <textarea v-model="contactForm.message" placeholder="Your Request" class="p-3 rounded-lg text-black h-32" required></textarea>
            <button type="submit" class="bg-sky-500 text-white px-6 py-3 rounded-full hover:bg-sky-600">Send Message</button>
          </form>
          <div class="mt-8 space-x-4">
            <span class="text-lg">Follow us:</span>
            <a href="#" class="text-sky-400 hover:text-white">YouTube</a> |
            <a href="#" class="text-pink-400 hover:text-white">Instagram</a> |
            <a href="#" class="text-blue-400 hover:text-white">Facebook</a> |
            <a href="#" class="text-purple-400 hover:text-white">TikTok</a> |
            <a href="#" class="text-gray-400 hover:text-white">X</a>
          </div>
        </div>
      </section>
    </main>

    <footer class="w-full p-5 text-center text-sm text-gray-500">
      &copy; 2025 Brand Name. All rights reserved.
    </footer>
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from 'vue';
import { Carousel, Slide, Pagination, Navigation } from 'vue3-carousel';
import 'vue3-carousel/dist/carousel.css';

const isPlaying = ref(false);
const audioPlayer = ref(null);
const volume = ref(0.5);

// Play music function
const playMusic = (src) => {
  if (audioPlayer.value) {
    audioPlayer.value.pause(); // Stop any currently playing music
  }

  // Create a new audio element
  audioPlayer.value = new Audio(src);
  audioPlayer.value.volume = volume.value; // Set initial volume
  audioPlayer.value.play(); // Play the music
  isPlaying.value = true; // Update playing state

  // Listen for when the music ends
  audioPlayer.value.addEventListener('ended', () => {
    isPlaying.value = false;
  });
};

// Toggle pause/resume function
const togglePause = () => {
  if (audioPlayer.value) {
    if (isPlaying.value) {
      audioPlayer.value.pause(); // Pause the music
    } else {
      audioPlayer.value.play(); // Resume the music
    }
    isPlaying.value = !isPlaying.value; // Toggle playing state
  }
};

// Update volume function
const setVolume = () => {
  if (audioPlayer.value) {
    audioPlayer.value.volume = volume.value; // Update audio volume
  }
};

// Dynamic slider track color
const sliderStyle = computed(() => {
  const percent = volume.value * 100; // Convert volume (0-1) to percentage (0-100)
  return {
    '--track-color': `linear-gradient(90deg, #ef4444 ${percent}%, #d1d5db ${percent}%)`,
  };
});

const video = ref(null);
const currentTime = ref(0);
const duration = ref(0);

// Toggle play/pause
const togglePlay = () => {
  if (video.value.paused) {
    video.value.play();
    isPlaying.value = true;
  } else {
    video.value.pause();
    isPlaying.value = false;
  }
};

// Update time during playback
const updateTime = () => {
  currentTime.value = video.value.currentTime;
};

// Set video duration
const setDuration = () => {
  if (video.value?.duration && !isNaN(video.value.duration)) {
    duration.value = video.value.duration;
  }
};

const handleCanPlay = () => {
  setDuration(); // Ensure duration is set once the video can play
};

// Seek video on slider change
const seekVideo = () => {
  video.value.currentTime = currentTime.value;
};

// Format time (mm:ss)
const formatTime = (time) => {
  const minutes = Math.floor(time / 60);
  const seconds = Math.floor(time % 60).toString().padStart(2, '0');
  return `${minutes}:${seconds}`;
};


const carouselConfig = {
  itemsToShow: 1,
  snapAlign: 'center',
  wrapAround: true,
  breakpoints: {
    768: { itemsToShow: 3 },
    1024: { itemsToShow: 4 }
  },
  gap: 16,
  height: 400
};
const contactForm = ref({
  name: '',
  email: '',
  message: ''
});

const menuOpen = ref(false);
const musicalNotes = ref([]);
const currentSongs = ref([]);
const selectedType = ref('personalized');

const pastelColors = ['text-pink-400', 'text-sky-400', 'text-purple-400', 'text-teal-400', 'text-indigo-400', 'text-yellow-400'];

const personalizedSongs = [
  { title: 'Birthday Songs', description: 'Joyful tunes to celebrate special moments.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music1.mp3" },
  { title: 'Wedding Songs', description: 'Romantic melodies for a perfect ceremony.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music2.mp3" },
  { title: 'Farewell Songs', description: 'Heartfelt harmonies to say goodbye.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music3.mp3" },
  { title: 'Love Songs', description: 'Soulful ballads to express your feelings.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music1.mp3" },
  { title: 'Children\'s Songs', description: 'Fun and catchy rhymes for kids.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music2.mp3" },
  { title: 'Party Songs', description: 'Upbeat tracks to keep the party going.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music3.mp3" },
  { title: 'Fun Songs', description: 'Playful sounds for lighthearted moments.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music1.mp3" },
  { title: 'Motivational Songs', description: 'Empowering anthems to inspire you.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music2.mp3" },
  { title: '...and much more', description: 'A wide range of tunes for every occasion.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music3.mp3" }
];

const businessSongs = [
  { title: 'Advertising Jingles', description: 'Catchy and memorable tunes to promote your brand and products.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music1.mp3" },
  { title: 'Film Music', description: 'Evocative soundtracks to enhance the emotion and impact of your movie scenes.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music2.mp3" },
  { title: 'Content Background Music', description: 'Perfect audio accompaniments for your social media content on Instagram, YouTube, TikTok, and more.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music3.mp3" },
  { title: 'Background Music', description: 'Ambient music designed for yoga studios, massage parlors, dance classes, fitness centers, and more.', color: pastelColors[Math.floor(Math.random() * pastelColors.length)], musicSrc: "/audio/music1.mp3" },
];

const toggleSongs = (type) => {
  selectedType.value = type;
  currentSongs.value = type === 'personalized' ? personalizedSongs : businessSongs;
};

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value;
};

const closeMenu = () => {
  menuOpen.value = false;
};

const columnSpans = personalizedSongs.map(() => getRandomSpan());
const rowSpans = personalizedSongs.map(() => getRandomSpan());

function getRandomSpan() {
  const spans = ['span 1', 'span 2', 'span 3'];
  return spans[Math.floor(Math.random() * spans.length)];
}

const generateNotes = () => {
  const symbols = ['♪', '♫', '♬', '♩'];
  const section = document.getElementById('features');
  const rect = section.getBoundingClientRect();

  musicalNotes.value = Array.from({ length: 30 }).map(() => {
    const angle = Math.random() * 2 * Math.PI;
    const distance = Math.random() * 300 + 50;
    const x = Math.cos(angle) * distance;
    const y = Math.sin(angle) * distance;

    // Random position within the section
    const randomTop = Math.random() * rect.height;
    const randomLeft = Math.random() * rect.width;
    const delay = Math.random() * 3; // Stagger explosions

    return {
      symbol: symbols[Math.floor(Math.random() * symbols.length)],
      style: `
        top: ${rect.top + window.scrollY + randomTop}px;
        left: ${rect.left + window.scrollX + randomLeft}px;
        font-size: ${Math.random() * 2 + 1.5}rem;
        --translate-x: ${x}px;
        --translate-y: ${y}px;
        animation-delay: ${delay}s;
      `
    };
  });
};

const handleScroll = () => {
  [features, about, contact, video].forEach(section => {
    if (section.value) {
      const rect = section.value.getBoundingClientRect();
      if (rect.top < window.innerHeight * 0.75) {
        section.value.classList.add('opacity-100', 'translate-y-0');
      }
    }
  });
};
// Refresh the notes every 6 seconds
setInterval(generateNotes, 6000);

onMounted(() => {

  generateNotes();
  window.addEventListener('scroll', handleScroll);
  handleScroll();

  toggleSongs('personalized');

  const sections = document.querySelectorAll('section');

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.remove('opacity-0', 'translate-y-10');
      }
    });
  }, { threshold: 0.3 });

  sections.forEach(section => observer.observe(section));
});
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Fugaz+One&display=swap');


@keyframes float-outwards {
  0% { transform: translate(0, 0); opacity: 1; }
  100% { transform: translate(var(--translate-x), var(--translate-y)); opacity: 0; }
}

.song-menu-container {
  display: grid;
  gap: 1.5rem;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: minmax(150px, auto);
  max-height: 70vh;
  overflow: hidden;
}
.song-card:nth-child(1) { grid-column: span 2; grid-row: span 1; }
.song-card:nth-child(2) { grid-column: span 1; grid-row: span 2; }
.song-card:nth-child(3) { grid-column: span 1; grid-row: span 1; }
.song-card:nth-child(4) { grid-column: span 2; grid-row: span 2; }
.song-card:nth-child(5) { grid-column: span 1; grid-row: span 1; }
.song-card:nth-child(6) { grid-column: span 2; grid-row: span 1; }
.song-card:nth-child(7) { grid-column: span 1; grid-row: span 2; }
.song-card:nth-child(8) { grid-column: span 1; grid-row: span 1; }

.note {
  position: absolute;
  font-size: 4rem;
  color: #CD7F32;
  animation: float-outwards 6s ease-out forwards;
  animation-iteration-count: infinite;
  z-index: 0;
}

.carousel {
  --vc-nav-background: rgba(0, 0, 0, 0.3);
  --vc-nav-color: white;
  --vc-nav-color-hover: #e5e5e5;
  --vc-nav-border-radius: 50%;
  --vc-nav-width: 40px;
  --vc-nav-height: 40px;
}

input[type="range"] {
  appearance: none;
  background: #ddd;
  height: 5px;
  border-radius: 5px;
}

input[type="range"]::-webkit-slider-thumb {
  appearance: none;
  background: #0284c7;
  width: 15px;
  height: 15px;
  border-radius: 50%;
  cursor: pointer;
}

/* Custom styles for the volume slider */
.volume-slider {
  -webkit-appearance: none; /* Remove default styling */
  appearance: none;
  width: 100px; /* Adjust width as needed */
  height: 6px; /* Adjust height as needed */
  background: var(--track-color, #d1d5db); /* Use CSS variable for dynamic color */
  border-radius: 5px; /* Rounded corners */
  outline: none;
  opacity: 0.7;
  transition: opacity 0.2s;
}

.volume-slider:hover {
  opacity: 1; /* Fully opaque on hover */
}

/* Custom thumb (slider handle) */
.volume-slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 16px; /* Adjust size as needed */
  height: 16px;
  background: #ef4444; /* Red color */
  border: 2px solid white; /* Add a border for better visibility */
  border-radius: 50%; /* Circular thumb */
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* Add a subtle shadow */
}

.volume-slider::-moz-range-thumb {
  width: 16px;
  height: 16px;
  background: #ef4444; /* Red color */
  border: 2px solid white; /* Add a border for better visibility */
  border-radius: 50%;
  cursor: pointer;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* Add a subtle shadow */
}

/* Custom track color */
.volume-slider::-webkit-slider-runnable-track {
  background: var(--track-color, #d1d5db); /* Use CSS variable for dynamic color */
  border-radius: 5px;
}

.volume-slider::-moz-range-track {
  background: var(--track-color, #d1d5db); /* Use CSS variable for dynamic color */
  border-radius: 5px;
}
</style>
