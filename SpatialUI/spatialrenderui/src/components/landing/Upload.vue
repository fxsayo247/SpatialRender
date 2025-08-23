<template>
  <div
    class="upload-container"
    @click="triggerFileInput"
    @dragover.prevent="onDragOver"
    @dragleave.prevent="onDragLeave"
    @drop.prevent="onDrop"
    :class="{ 'is-dragging': isDragging, 'has-files': uploadedFiles.length > 0 }"
  >
    <!-- Hidden file input, triggered programmatically -->
    <input
      type="file"
      ref="fileInput"
      @change="onFileSelect"
      multiple
      accept="image/*,.zip,application/zip"
      style="display: none;"
    />

    <!-- Initial upload prompt -->
    <div v-if="uploadedFiles.length === 0" class="upload-content">
      <p>Drag & drop your images or .zip files here</p>
      <p>or</p>
      <button type="button" class="browse-button">Browse Files</button>
    </div>

    <!-- Image collage display -->
    <div v-else class="image-collage">
      <div v-for="item in uploadedFiles" :key="item.url" class="collage-item">
        <img v-if="item.file.type.startsWith('image/')" :src="item.url" :alt="item.file.name" class="collage-image" />
        <div v-else class="file-item">
          <span>{{ item.file.name }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'UploadFile',
  data() {
    return {
      isDragging: false,
      uploadedFiles: [],
    };
  },
  methods: {
    triggerFileInput() {
      // Programmatically click the hidden file input element
      this.$refs.fileInput.click();
    },
    onDragOver() {
      // This event is necessary to allow a drop.
      // We set a flag to provide visual feedback to the user.
      this.isDragging = true;
    },
    onDragLeave() {
      this.isDragging = false;
    },
    onDrop(event) {
      this.isDragging = false;
      // Get the files from the drop event
      const files = event.dataTransfer.files;
      this.handleFiles(files);
    },
    onFileSelect(event) {
      // Get the files from the file input dialog
      const files = event.target.files;
      this.handleFiles(files);
    },
    handleFiles(files) {
      // Process the list of files (from either drop or select)
      for (const file of files) {
        this.uploadedFiles.push(
            {
                file: file,
                url: URL.createObjectURL(file)
            }
        );
      }
      console.log('Selected files:', this.uploadedFiles);
      // In a real application, you would trigger the upload process here.
      this.$emit('files-uploaded', this.uploadedFiles);
    }
  }
};
</script>

<style scoped>
.upload-container {
  box-sizing: border-box;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  max-width: 1400px;
  margin: 2rem auto;
  height: 700px;
  border: 2px dashed #ccc;
  border-radius: 10px;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out, border-color 0.2s ease-in-out;
  background-color: #f9f9f9;
  top: 1rem;
}

.upload-container.has-files {
  align-items: flex-start;
  justify-content: flex-start;
  padding: 1rem;
  overflow-y: auto;
}

.upload-container:hover,
.upload-container.is-dragging {
  background-color: #f0f8ff;
  border-color: #007bff;
}

.upload-content {
  text-align: center;
  color: #555;
  pointer-events: none; /* Prevents text from interfering with click event */
}

.browse-button {
  margin-top: 1rem;
  padding: 10px 20px;
  border: 1px solid #007bff;
  background-color: #007bff;
  color: white;
  border-radius: 5px;
  font-size: 1rem;
  transition: background-color 0.2s;
}

.image-collage {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  width: 100%;
}

.collage-item {
  flex: 1 1 200px; /* Grow and shrink, with a base size */
  /* height: 200px; */
  border-radius: 8px;
  overflow: hidden;
}

.collage-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.file-item {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #e9ecef;
  padding: 1rem;
  text-align: center;
  word-break: break-word;
  color: #495057;
}
</style>

