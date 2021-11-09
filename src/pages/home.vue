<template>
  <div class="mb-body">
    <Form @onSubmit="handleSubmit" />
    <List @onRemove="handleRemove" :items="items" />
  </div>
</template>

<script>
import Form from '@/components/Notes/Form'
import List from '@/components/Notes/List'

export default {
  components: {
    Form,
    List
  },
  data() {
    return {
      items: [
        {
          title: 'Learn Vue3',
          tags: ['work']
        },
        {
          title: 'English course',
          tags: ['work', 'home']
        }
      ]
    }
  },
  mounted() {
    this.getItems()
  },
  watch: {
    items: {
      handler(updatedList) {
        localStorage.setItem('notes', JSON.stringify(updatedList))
      },
      deep: true
    }
  },
  methods: {
    handleSubmit(note) {
      this.items.push({ title: note.title, tags: note.tags })
    },
    handleRemove(index) {
      this.items.splice(index, 1)
    },
    getItems() {
      const localNotes = localStorage.getItem('notes')
      if (localNotes) {
        this.items = JSON.parse(localNotes)
      }
    }
  }
}
</script>
