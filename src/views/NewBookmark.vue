<template>
  <div class="form-area card border p-2">
    <div class="mb-3">
      <label for="title" class="form-label">Başlık</label>
      <input
        type="text"
        class="form-control"
        id="title"
        placeholder="kablosuzkedi..."
        v-model="userData.title"
      />
    </div>
    <div class="mb-3">
      <label for="url" class="form-label">URL</label>
      <input
        type="text"
        class="form-control"
        id="url"
        placeholder="https://..."
        v-model="userData.url"
      />
    </div>
    <div class="mb-3">
      <label for="description" class="form-label">Açıklama</label>
      <textarea
        class="form-control"
        id="description"
        rows="3"
        placeholder="Bu var ya..."
        v-model="userData.description"
      ></textarea>
    </div>
    <div class="d-flex justify-content-end align-items-center">
      <button
        class="btn btn-sm btn-secondary me-2"
        @click="$router.push({ name: 'HomePage' })"
      >
        İptal
      </button>
      <button class="btn btn-sm btn-primary" @click="onSave">Kaydet</button>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        userData: {
          title: null,
          url: null,
          description: null,
        },
      }
    },
    methods: {
      onSave() {
        console.log(this.userData);
        this.$appAxios.post("/bookmarks", this.userData).then(save_response => {
          console.log("save_response", save_response);
          this.resetData();
          this.$router.push("/");
        });
      },
      resetData() {
        Object.keys(this.userData).forEach(key => (this.userData[key] = null));
      },
    },
  }
</script>