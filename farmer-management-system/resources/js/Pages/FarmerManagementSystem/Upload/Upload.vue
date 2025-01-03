<script setup>
import PannelLayout from '@/Layouts/PannelLayout.vue';
import { ref } from 'vue';
import axios from 'axios';

// Ref for the selected file
const selectedFile = ref(null);
const selectedFileName = ref(''); // To store the name of the selected file

const handleFileChange = (event) => {
    const file = event.target.files[0];
    if (file) {
        selectedFile.value = file;
        selectedFileName.value = file.name; // Update the file name
    } else {
        selectedFile.value = null;
        selectedFileName.value = ''; // Reset if no file selected
    }
};

const uploadFile = async () => {
    if (!selectedFile.value) {
        alert('Please select a file to upload.');
        return;
    }

    const formData = new FormData();
    formData.append('module', selectedFile.value);

    try {
        const response = await axios.post('/upload-zip', formData, {
            headers: {
                'Content-Type': 'multipart/form-data',
            },
        });
        alert(response.data.message);
        // Reset after successful upload
        selectedFile.value = null;
        selectedFileName.value = '';
    } catch (error) {
        alert(error.response?.data?.error || 'An error occurred while uploading the file.');
    }
};
</script>

<template>
    <PannelLayout>
        <h1>Upload Page</h1>

        <div class="flex items-center justify-center w-full">
            <label for="dropzone-file"
                class="flex flex-col items-center justify-center w-full h-64 border-2 border-gray-300 border-dashed rounded-lg cursor-pointer bg-gray-50 dark:hover:bg-gray-800 dark:bg-gray-700 hover:bg-gray-100 dark:border-gray-600 dark:hover:border-gray-500 dark:hover:bg-gray-600">
                <div class="flex flex-col items-center justify-center pt-5 pb-6">
                    <svg class="w-8 h-8 mb-4 text-gray-500 dark:text-gray-400" aria-hidden="true"
                        xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 16">
                        <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M13 13h3a3 3 0 0 0 0-6h-.025A5.56 5.56 0 0 0 16 6.5 5.5 5.5 0 0 0 5.207 5.021C5.137 5.017 5.071 5 5 5a4 4 0 0 0 0 8h2.167M10 15V6m0 0L8 8m2-2 2 2" />
                    </svg>
                    <p class="mb-2 text-sm text-gray-500 dark:text-gray-400">
                        <span class="font-semibold">Click to upload</span> or drag and drop
                    </p>
                    <p class="text-xs text-gray-500 dark:text-gray-400">ZIP files only</p>
                </div>
                <input id="dropzone-file" type="file" class="hidden" @change="handleFileChange" />
            </label>
        </div>

        <!-- Display selected file name -->
        <div v-if="selectedFileName" class="mt-2 text-center text-gray-600 dark:text-gray-400">
            Selected file: <span class="font-semibold">{{ selectedFileName }}</span>
        </div>

        <div class="mt-4">
            <button class="px-4 py-2 text-white bg-blue-500 rounded hover:bg-blue-600"
                :class="{ 'opacity-50 cursor-not-allowed': !selectedFile }" @click="uploadFile"
                :disabled="!selectedFile">
                Upload File
            </button>
        </div>
    </PannelLayout>
</template>
