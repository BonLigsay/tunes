<template>
    <AppLayout title="Dashboard">
        <div class="container mx-auto px-6 py-8">
            <h1 class="text-4xl font-bold text-orange-600 mb-8">Manage Requests</h1>


            <!-- Requests Table -->
            <div>
                <!-- Table (visible on screens `sm` and larger) -->
                <div class="hidden sm:block overflow-x-auto">
                <table class="min-w-full border border-gray-300">
                    <thead class="bg-gray-300 text-center">
                    <tr>
                        <th class="px-6 py-3 text-sm font-medium text-gray-700 uppercase">ID</th>
                        <th class="px-6 py-3 text-sm font-medium text-gray-700 uppercase">Name</th>
                        <th class="px-6 py-3 text-sm font-medium text-gray-700 uppercase">Contact</th>
                        <th class="px-6 py-3 text-sm font-medium text-gray-700 uppercase">Address</th>
                        <th class="px-6 py-3 text-sm font-medium text-gray-700 uppercase">Details</th>
                        <th class="px-6 py-3 text-sm font-medium text-gray-700 uppercase">Date</th>
                        <th class="px-6 py-3 text-sm font-medium text-gray-700 uppercase">Actions</th>
                    </tr>
                    </thead>
                    <tbody class="divide-y divide-gray-200">
                    <tr v-for="request in requests" :key="request.id">
                        <td class="px-6 py-4 text-sm text-gray-900">{{ request.id }}</td>
                        <td class="px-6 py-4 text-sm text-gray-900">{{ request.name }}</td>
                        <td class="px-6 py-4 text-sm text-gray-900">{{ request.contact }}</td>
                        <td class="px-6 py-4 text-sm text-gray-900">{{ request.address }}</td>
                        <td class="px-6 py-4 text-sm text-gray-900">{{ request.details }}</td>
                        <td class="px-6 py-4 text-sm text-gray-900">Feb 05 - Feb 10</td>
                        <td class="px-6 py-4 text-sm text-gray-900">
                        <div class="flex flex-row gap-2 items-center justify-center">
                            <button @click="openEditModal(request)" class="px-3 py-1 bg-green-600 text-white rounded-lg hover:bg-green-700">Edit</button>
                            <button @click="deleteRequest(request.id)" class="px-3 py-1 bg-red-600 text-white rounded-lg hover:bg-red-700">Delete</button>
                        </div>
                        </td>
                    </tr>
                    </tbody>
                </table>
                </div>

                <!-- Mobile-friendly Card Layout (visible on small screens `sm:hidden`) -->
                <div class="sm:hidden flex flex-col gap-4">
                <div v-for="request in requests" :key="request.id" class="bg-white p-4 rounded-lg shadow-md border border-gray-300">
                    <p class="text-gray-700"><strong>ID:</strong> {{ request.id }}</p>
                    <p class="text-gray-700"><strong>Name:</strong> {{ request.name }}</p>
                    <p class="text-gray-700"><strong>Contact:</strong> {{ request.contact }}</p>
                    <p class="text-gray-700"><strong>Address:</strong> {{ request.address }}</p>
                    <p class="text-gray-700"><strong>Details:</strong> {{ request.details }}</p>
                    <p class="text-gray-700"><strong>Date:</strong> Feb 05 - Feb 10</p>
                    <div class="flex gap-2 mt-2">
                    <button @click="openEditModal(request)" class="px-3 py-1 bg-green-600 text-white rounded-lg hover:bg-green-700 w-full">Edit</button>
                    <button @click="deleteRequest(request.id)" class="px-3 py-1 bg-red-600 text-white rounded-lg hover:bg-red-700 w-full">Delete</button>
                    </div>
                </div>
                </div>
            </div>

            <!-- Create/Edit Modal -->
            <div v-if="isModalOpen" class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
                <div class="bg-white p-8 rounded-lg shadow-lg w-full max-w-md">
                    <h3 class="text-2xl font-bold text-orange-600 mb-6">
                    {{ isEditing ? 'Edit Request' : 'Create Request' }}
                    </h3>

                    <!-- Form -->
                    <form @submit.prevent="submitForm">
                    <!-- Name Field -->
                    <div class="mb-4">
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
                    <div class="mb-4">
                        <label for="contact" class="block text-sm font-medium text-gray-700">Contact No.</label>
                        <input
                        type="tel"
                        id="contact"
                        v-model="form.contact"
                        class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-orange-500 focus:border-orange-500"
                        required
                        />
                    </div>

                    <!-- Address Field -->
                    <div class="mb-6">
                        <label for="address" class="block text-sm font-medium text-gray-700">Address</label>
                        <input
                        type="text"
                        id="address"
                        v-model="form.address"
                        class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-lg shadow-sm focus:outline-none focus:ring-orange-500 focus:border-orange-500"
                        required
                        />
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
                        type="submit"
                        class="px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition duration-300"
                        >
                        {{ isEditing ? 'Update' : 'Create' }}
                        </button>
                    </div>
                    </form>
                </div>
            </div>
        </div>
    </AppLayout>
  
</template>

<script setup>
import { ref } from 'vue';
import AppLayout from '@/Layouts/AppLayout.vue';

// Sample data
const requests = ref([
  { id: 1, name: 'John Doe', contact: '123-456-7890', address: '123 Main St',  details: 'Lorem ipsum dolor sit amet consectetur adipisicing elit.',},
  { id: 2, name: 'Jane Smith', contact: '987-654-3210', address: '456 Elm St', details: 'Lorem ipsum dolor sit amet consectetur adipisicing elit.',},
]);

// Modal state
const isModalOpen = ref(false);
const isEditing = ref(false);

// Form data
const form = ref({
  id: null,
  name: '',
  contact: '',
  address: '',
  details: '',
});

// Open create modal
const openCreateModal = () => {
  resetForm();
  isEditing.value = false;
  isModalOpen.value = true;
};

// Open edit modal
const openEditModal = (request) => {
  form.value = { ...request };
  isEditing.value = true;
  isModalOpen.value = true;
};

// Close modal
const closeModal = () => {
  isModalOpen.value = false;
  resetForm();
};

// Reset form
const resetForm = () => {
  form.value = {
    id: null,
    name: '',
    contact: '',
    address: '',
  };
};

// Submit form (create or update)
const submitForm = () => {
  if (isEditing.value) {
    // Update request
    const index = requests.value.findIndex((r) => r.id === form.value.id);
    if (index !== -1) {
      requests.value[index] = { ...form.value };
    }
  } else {
    // Create new request
    const newRequest = { ...form.value, id: requests.value.length + 1 };
    requests.value.push(newRequest);
  }
  closeModal();
};

// Delete request
const deleteRequest = (id) => {
  requests.value = requests.value.filter((request) => request.id !== id);
};
</script>

<style scoped>
/* Add custom styles here if needed */
</style>