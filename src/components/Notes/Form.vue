<template>
  <div class="note-form__wrapper">
    <form class="note-form" @submit.prevent="onSubmit">
      <textarea v-model="value" placeholder="Type ur note" required />
      <TagsList
        :items="tags"
        :activeItems="activeTags"
        @onItemClick="handleTagClick"
      />
      <button class="btn btnPrimary" type="submit">Add new note</button>
    </form>
  </div>
</template>

<script>
import TagsList from '@/components/UI/TagsList'

export default {
  components: {
    TagsList
  },
  data() {
    return {
      value: '',
      tags: ['home', 'work', 'travel'],
      activeTags: []
    }
  },
  methods: {
    onSubmit() {
      this.$emit('onSubmit', { title: this.value, tags: this.activeTags })
      this.value = ''
      this.activeTags = []
    },
    handleTagClick(tag) {
      const index = this.activeTags.indexOf(tag)
      if (index > -1) {
        this.activeTags.splice(index, 1)
      } else {
        this.activeTags.push(tag)
      }
    }
  }
}
</script>

<style lang="scss">
.note-form__wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.note-form {
  max-width: 600px;
  display: flex;
  flex-direction: column;
  width: 100%;
}
</style>
