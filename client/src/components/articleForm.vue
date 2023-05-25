<template>
  <div class="flex items-center justify-center p-12">
    <div class="mx-auto w-full max-w-[550px]">
      <form @submit.prevent="article ? updateArticle() : addArticle()">
        <div class="mb-5">
          <!-- title -->
          <label for="name" class="mb-3 block text-base font-medium text-[#07074D]">
            Article Title
          </label>
          <input
            v-model="newArticle.title"
            type="text"
            name="title"
            id="title"
            placeholder="Article Title"
            class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
          />
        </div>

        <!-- content -->
        <div class="mb-5">
          <label for="description" class="mb-3 block text-base font-medium text-[#07074D]">
            Content
          </label>
          <textarea
            v-model="newArticle.content"
            rows="4"
            name="content"
            id="content"
            placeholder="Article's Content"
            class="w-full resize-none rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
          ></textarea>
        </div>

        <!-- imgUrl -->
        <div class="mb-5">
          <label for="imgUrl" class="mb-3 block text-base font-medium text-[#07074D]">
            Image
          </label>
          <input
            v-model="newArticle.imgUrl"
            type="text"
            name="imgUrl"
            id="imgUrl"
            placeholder="Article's imgUrl"
            class="w-full rounded-md border border-[#e0e0e0] bg-white py-3 px-6 text-base font-medium text-[#6B7280] outline-none focus:border-[#6A64F1] focus:shadow-md"
          />
        </div>

        <!-- category -->
        <div class="mb-5">
          <label for="categoryId" class="mb-3 block text-base font-medium text-[#07074D]">
            Category
          </label>
          <select id="categoryId" class="form-select" required v-model="newArticle.categoryId">
            <option value="" selected disabled>-- Select Category --</option>
            <option v-for="(category, i) in categories" :key="i" :value="category.id">
              {{ category.name }}
            </option>
          </select>
        </div>

        <div>
          <button
            type="sumbit"
            class="hover:shadow-form rounded-md bg-[#6A64F1] py-3 px-8 text-base font-semibold text-white outline-none"
          >
            Submit
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  props: ['categories', 'article'],
  data() {
    return {
      newArticle: {
        title: '',
        content: '',
        imgUrl: '',
        categoryId: ''
      }
    }
  },

  methods: {
    addArticle() {
      this.$emit('addArticle', this.newArticle)
    },
    updateArticle() {
      this.$emit('updateArticle', this.newArticle, this.article.id)
    }
  },
  created() {
    if (this.article) {
      this.newArticle.title = this.article.title
      this.newArticle.content = this.article.content
      this.newArticle.imgUrl = this.article.imgUrl
      this.newArticle.categoryId = this.article.categoryId
    }
  }
}
</script>

<style></style>
