<template>
  <div class="container">
    <div v-if="error">
      {{ error }}
    </div>
    <ul v-else>
      These are the cards:
      <li v-for="card in cards" :key="card.id">
        {{ card.attributes.Title }}
        {{ card.attributes.body }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      cards: [],
      error: null,
    }
  },

  async fetch() {
    try {
      const response = await this.$axios.get('/cards')
      this.cards = response.data.data
    } catch (error) {
      this.error = error
      console.error(error)
    }
  },
}
</script>
