<template>
  <div class="min-h-screen overflow-hidden">
    <!-- Hero Section with Video Background -->
    <!-- Remove h-screen from the parent container to allow natural vertical stacking -->
    <div class="relative overflow-hidden">
      <!-- Content Section (now takes natural height) -->
      <div
        class="relative z-10 min-h-[60vh] flex flex-col justify-center bg-cover bg-center bg-no-repeat"
        style="background-image: url('images/9.jpg');"
      >
        <div class="container mx-auto px-6 py-20 text-center bg-black bg-opacity-40 rounded-lg">
          <h1 class="text-5xl font-fugaz font-bold text-blue-400 mb-6">
            Welcome to {{ appName }}
          </h1>
          <p class="text-xl font-fugaz text-blue-400 mb-8">
            Your ultimate destination for music, creativity, and inspiration. Join us and explore the world of melodies.
          </p>
          <a
            class="px-8 py-3 bg-blue-500 font-fugaz text-white rounded-lg text-lg transition duration-300"
          >
            Scroll Down to Explore
          </a>
        </div>
      </div>


      <!-- Video Section (explicit height) -->
      <div class="relative z-0 h-[50vh]"> <!-- Adjust height as needed (e.g., h-[50vh], h-screen, etc.) -->
        <video
          ref="videoPlayer"
          autoplay
          muted
          loop
          class="w-full h-full object-cover"
        >
          <source src="/videos/example.mp4" type="video/mp4">
        </video>
      </div>
    </div>  

    <!-- About the Artist -->
    <div class="relative bg-white py-20">
      <div class="container mx-auto px-6 text-justify">
        <h2 class="text-5xl font-fugaz font-bold text-orange-600 mb-6">
          About the Artist
        </h2>
        <p class="text-xl font-fugaz text-gray-700 mb-8">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsum maxime cupiditate commodi quam. Obcaecati tempora minima porro molestias labore itaque officia corporis alias, provident quaerat earum dignissimos dolores, tenetur qui!
        </p>
        <vue-marquee-slider
          id="marquee-slider"
            :speed="10500"
            :width="300"
            :space="50"
            >            
            <div class="w-full flex justify-center items-center"><img src="/images/2.jpeg"/></div>
            <div class="w-full flex justify-center items-center"><img src="/images/3.jpg"/></div>
            <div class="w-full flex justify-center items-center"><img src="/images/4.jpg"/></div>
            <div class="w-full flex justify-center items-center"><img src="/images/5.webp"/></div>
            <div class="w-full flex justify-center items-center"><img src="/images/6.jpg"/></div>
            <div class="w-full flex justify-center items-center"><img src="/images/7.webp"/></div>
            <div class="w-full flex justify-center items-center"><img src="/images/8.jpg"/></div>
        </vue-marquee-slider>
        <p class="text-xl font-fugaz text-gray-700 mt-8">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsum maxime cupiditate commodi quam. Obcaecati tempora minima porro molestias labore itaque officia corporis alias, provident quaerat earum dignissimos dolores, tenetur qui!
        </p> 
      </div>         
    </div>
    
    <!-- What I can offer you -->
    <div class="relative font-fugaz bg-gray-300 py-20">
      <div class="container mx-auto px-6">
        <!-- Section Title -->
        <h2 class="text-5xl font-fugaz font-bold text-orange-600 mb-6 text-center md:text-left">
          What I Can Offer You
        </h2>

        <!-- Product Containers -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <!-- Container 1 -->
          <div class="bg-white p-6 rounded-lg shadow-md">
            <h3 class="text-2xl font-bold text-orange-600 mb-4">Product Category 1</h3>
            <ul class="text-gray-700 mb-6">
              <li class="mb-2">Product 1</li>
              <li class="mb-2">Product 2</li>
              <li class="mb-2">Product 3</li>
              <li class="mb-2">Product 4</li>
            </ul>
            <img src="/images/01.jpeg" alt="Product 1" class="w-full h-auto rounded-lg">
            <button
            @click="playMusic('/audio/music1.mp3')"
            class="w-full mt-4 px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition duration-300"
            >Play Music</button>
          </div>

          <!-- Container 2 -->
          <div class="bg-white p-6 rounded-lg shadow-md">
            <h3 class="text-2xl font-bold text-orange-600 mb-4">Product Category 2</h3>
            <ul class="text-gray-700 mb-6">
              <li class="mb-2">Product 1</li>
              <li class="mb-2">Product 2</li>
              <li class="mb-2">Product 3</li>
              <li class="mb-2">Product 4</li>
            </ul>
            <img src="/images/02.jpg" alt="Product 2" class="w-full h-auto rounded-lg">
            <button
            @click="playMusic('/audio/music2.mp3')"
            class="w-full mt-4  px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition duration-300"
            >
              Play Music
            </button>
          </div>

          <!-- Container 3 -->
          <div class="bg-white p-6 rounded-lg shadow-md">
            <h3 class="text-2xl font-bold text-orange-600 mb-4">Product Category 3</h3>
            <ul class="text-gray-700 mb-6">
              <li class="mb-2">Product 1</li>
              <li class="mb-2">Product 2</li>
              <li class="mb-2">Product 3</li>
              <li class="mb-2">Product 4</li>
            </ul>
            <img src="/images/03.jpg" alt="Product 3" class="w-full h-auto rounded-lg">
            <button
              @click="playMusic('/audio/music3.mp3')"
              class="w-full mt-4 px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition duration-300"
            >
              Play Music
            </button>
          </div>

          <!-- Volume Control -->
          <div class="absolute flex items-center  bottom-4 right-4 z-20z-20">
            <!-- Pause Button -->
            <button
              @click="togglePause"
              class="mr-4 px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition duration-300"
            >
              {{ isPlaying ? 'Pause' : 'Resume' }}
            </button>

            <!-- Volume Slider -->
            <div class="space-x-2 bg-white bg-opacity-75 rounded-full p-2">
              <input
                type="range"
                  id="volume"
                  min="0"
                  max="1"
                  step="0.1"
                  v-model="volume"
                  class="w-full volume-slider"
                  @input="setVolume"
                  :style="sliderStyle"
              />
            </div>
          </div>          
        </div>
      </div>
    </div>

    <!-- Request -->
    <div class="relative font-fugaz bg-white py-20">
      <div class="container flex flex-col items-center justify-center mx-auto px-6 text-justify">
        <h2 class="text-5xl font-fugaz font-bold text-orange-600 mb-6">
          I Can Make You A Song
        </h2>
        <p class="text-xl font-fugaz text-gray-700 mb-8">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Ipsum maxime cupiditate commodi quam. Obcaecati tempora minima porro molestias labore itaque officia corporis alias, provident quaerat earum dignissimos dolores, tenetur qui!
        </p>
        <button @click="openRequestModal" class="mr-4 px-4 py-2 bg-orange-600 text-white text-3xl rounded-lg hover:bg-red-700 transition duration-300">
          Request
        </button>
        <h2 class="mr-auto text-3xl font-fugaz font-bold text-orange-600 mt-10 mb-4">
          Contact Me For Inquiries
        </h2>
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <div class="bg-gray-300 p-6 rounded-lg shadow-md">
            <h3 class="text-2xl font-bold text-orange-600 mb-4">Email</h3>
            <p class="text-gray-700">L2w7A@example.com</p>
          </div>

          <div class="bg-gray-300 p-6 rounded-lg shadow-md">
            <h3 class="text-2xl font-bold text-orange-600 mb-4">Phone</h3>
            <p class="text-gray-700">+91 1234567890</p>
          </div>

          <div class="bg-gray-300 p-6 rounded-lg shadow-md">
            <h3 class="text-2xl font-bold text-orange-600 mb-4">Instagram</h3>
            <p class="text-gray-700">@user</p>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- Request Modal -->
  <div v-if="isRequestModalOpen" class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
    <div class="bg-white p-8 rounded-lg shadow-lg w-full max-w-4xl">
      <h3 class="text-2xl font-bold text-orange-600 mb-6">Request a Song</h3>

      <!-- Form -->
      <form @submit.prevent="openPaymentModal">
        
        <div class="flex flex-row gap-4 w-full mb-4"> 
            <!-- Name Field -->
          <div class="w-full">
            <label for="name" class="block text-sm font-medium text-gray-700">Name</label>
            <input
              type="text"
              id="name"
              v-model="form.name"
              class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-orange-500 focus:border-orange-500"
              required
            />
          </div>

          <!-- Contact No. Field -->
          <div class="w-full">
            <label for="contact" class="block text-sm font-medium text-gray-700">Contact No.</label>
            <input
              type="tel"
              id="contact"
              v-model="form.contact"
              class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-orange-500 focus:border-orange-500"
              required
            />
          </div>

          <!-- Email Field -->
          <div class="w-full">
            <label for="email" class="block text-sm font-medium text-gray-700">Email</label>
            <input
              type="text"
              id="email"
              v-model="form.email"
              class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-orange-500 focus:border-orange-500"
              required
            />
          </div>

          <!-- Address Field -->
          <div class="w-full">
            <label for="address" class="block text-sm font-medium text-gray-700">Address</label>
            <input
              type="text"
              id="address"
              v-model="form.address"
              class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-orange-500 focus:border-orange-500"
              required
            />
          </div>
        </div>

        <div class="flex flex-row gap-4 w-full mb-4">
          <div class="w-full">
            <label for="details" class="block text-sm font-medium text-gray-700">Details</label>
            <textarea
              type="textarea"
              id="details"
              v-model="form.details"
              class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-orange-500 focus:border-orange-500"
              required
            />
          </div>
        </div>

        <!-- Buttons -->
        <div class="flex justify-end space-x-4">
          <button
            type="button"
            @click="closeModal"
            class="px-4 py-2 bg-gray-500 text-white rounded-lg hover:bg-gray-600 transition duration-300"
          >
            Cancel
          </button>
          <button
            type="pay"
            class="px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition duration-300"
          >
            Pay
          </button>
        </div>
      </form>
    </div>
  </div>

  <!-- Payment Modal -->
    <div v-if="isPaymentModalOpen" class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
      <div class="bg-white p-8 rounded-lg shadow-lg w-full max-w-md">
        <h3 class="text-2xl font-bold text-orange-600 mb-6">Payment</h3>

        <!-- Payment Form -->
        <form @submit.prevent="submitForm">
          <!-- Card Details -->
          <div id="card-element" class="mb-4"></div>

          <!-- Buttons -->
          <div class="flex justify-end space-x-4">
            <button
              type="button"
              @click="closePaymentModal"
              class="px-4 py-2 bg-gray-500 text-white rounded-lg hover:bg-gray-600 transition duration-300"
            >
              Cancel
            </button>
            <button
              type="submit"
              class="px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition duration-300"
            >
              Pay Now
            </button>
          </div>
        </form>
      </div>
    </div>
    <Notification v-if="showNotification" :message="notificationMessage" />
</template>


<script setup>
import { ref, onMounted, computed } from 'vue';
import { VueMarqueeSlider } from 'vue3-marquee-slider';
import Notification from '@/Components/Notification.vue';

const showNotification = ref(false);
const notificationMessage = ref('');

// Modal states
const isRequestModalOpen = ref(false);
const isPaymentModalOpen = ref(false);

// Form data
const form = ref({
  name: '',
  contact: '',
  email: '',
  address: '',
  details: '',
  category: '',
});

// Open request modal
const openRequestModal = () => {
  isRequestModalOpen.value = true;
};

// Close request modal
const closeRequestModal = () => {
  isRequestModalOpen.value = false;
  resetForm();
};

// Open payment modal
const openPaymentModal = () => {
  if (form.value.name && form.value.contact && form.value.address) {
    isRequestModalOpen.value = false;
    isPaymentModalOpen.value = true;
  } else {
    alert('Please fill out all fields.');
  }
};

// Close payment modal
const closePaymentModal = () => {
  isPaymentModalOpen.value = false;
};

// Submit form
const submitForm = () => {
  console.log('Form submitted:', form.value);
  notificationMessage.value = "Payment successful";
  showNotification.value = true;
  setTimeout(() => {
    showNotification.value = false;
  }, 3000); // Hide notification after 3 seconds

  closePaymentModal();
  closeRequestModal();
};

// Reset form
const resetForm = () => {
  form.value = {
    name: '',
    contact: '',
    email: '',
    address: '',
    details: '',
    category: '',
  };
};

const appName = "Tunes";
const videoPlayer = ref(null);
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
</script>
<style scoped>
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