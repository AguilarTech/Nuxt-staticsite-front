<template>
  <div class="container min-h-100">
    <div class="py-12 bg-white">
      <div class="max-w-full mx-auto px-4 sm:px-6 lg:px-8">
        <div class="relative bg-white overflow-hidden">
          <div class="max-w-7xl mx-auto">
            <div
              class="relative z-10 pb-8 bg-white sm:pb-16 md:pb-20 lg:max-w-2xl lg:w-full lg:pb-28 xl:pb-32"
            >
              <svg
                class="hidden lg:block absolute right-0 inset-y-0 h-full w-48 text-white transform translate-x-1/2"
                fill="currentColor"
                viewBox="0 0 100 100"
                preserveAspectRatio="none"
                aria-hidden="true"
              >
                <polygon points="50,0 100,0 50,100 0,100" />
              </svg>
              <div>
                <div class="relative pt-6 px-4 sm:px-6 lg:px-8">
                  <nav
                    class="relative flex items-center justify-between sm:h-10 lg:justify-start"
                    aria-label="Global"
                  ></nav>
                </div>
              </div>
              <main
                class="mt-2 mx-auto max-w-7xl px-4 sm:mt-2 sm:px-6 md:mt-2 lg:mt-2 lg:px-8 xl:mt-2"
              >
                <div class="sm:text-center lg:text-left">
                  <h1
                    class="text-4xl tracking-tight font-extrabold text-gray-900 sm:text-5xl md:text-6xl"
                  >
                    <span class="block xl:inline">{{
                      siteSetup.mainHeading
                    }}</span>
                  </h1>

                  <h2
                    class="text-4xl tracking-tight font-extrabold text-blue-500 sm:text-5xl md:text-6xl"
                  >
                    <span class="block xl:inline">{{
                      siteSetup.mainSubheading
                    }}</span>
                  </h2>

                  <div
                    class="m-6 text-base sm:mt-5 sm:text-lg sm:max-w-xl sm:mx-auto md:mt-8 md:text-xl lg:mx-0"
                  >
                    <a
                      :href="siteSetup.mainTelephone"
                      class="rounded-full bg-yellow-400 hover:bg-yellow-300 hover:text-gray-50 py-2 px-6 text-white font-bold"
                    >
                      Call
                    </a>
                    <a
                      :href="siteSetup.mainEmail"
                      class="mx-4 rounded-full bg-yellow-400 hover:bg-yellow-300 hover:text-gray-50 py-2 px-6 text-white font-bold"
                    >
                      Email
                    </a>
                  </div>
                  <div
                    class="mt-5 sm:mt-8 sm:flex sm:justify-center lg:justify-start"
                  ></div>
                </div>
              </main>
            </div>
          </div>
          <div class="lg:absolute lg:inset-y-0 lg:right-0 lg:w-1/2">
            <img
              class="h-56 w-full object-cover sm:h-72 md:h-96 lg:w-full lg:h-full"
              :src="siteSetup.mainImageLink"
              alt="Voice Actor"
            />
          </div>
        </div>

        <div
          class="bg-white shadow-md rounded mt-5 mx-auto max-w-full sm:mt-12 p-4 md:mt-16 lg:mt-5 xl:mt-5"
          v-for="card in cards"
          :key="card.id"
        >
          <h3
            class="my-3 text-2xl tracking-tight font-extrabold text-blue-400 sm:text-2xl md:text-2xl"
          >
            {{ card.attributes.Title }}
          </h3>
          <div class="my-4">{{ card.attributes.body }}</div>
          <iframe
            width="100%"
            height="166"
            scrolling="no"
            frameborder="no"
            allow="autoplay"
            :src="card.attributes.Soundcloud_LInk"
          ></iframe>
        </div>
      </div>
    </div>
    <footer class="footer flex justify-center">
      <div class="p-4">
        <a
          href="https:/AguilarTech.io"
          class="px-4 py-1 text-sm text-blue-500 font-semibold rounded-full border border-blue-200 hover:text-white hover:bg-blue-200 hover:border-transparent focus:outline-none focus:ring-2 focus:ring-blue-600 focus:ring-offset-2"
          >Powered by AguilarTech.io</a
        >
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      cards: [],
      siteSetup: {},
      error: null,
    }
  },

  async fetch() {
    try {
      const Cardsresponse = await this.$axios.get('/cards')
      this.cards = Cardsresponse.data.data
    } catch (error) {
      this.error = error
      console.error(error)
    }

    try {
      const siteSetupResponse = await this.$axios.get('/site-setup')
      this.siteSetup = siteSetupResponse.data.data.attributes

      this.siteSetup.mainEmail = 'mailto:' + this.siteSetup.mainEmail
      this.siteSetup.mainTelephone = 'tel:' + this.siteSetup.mainTelephone

      console.log(`mainHeading: ${this.siteSetup.mainHeading}`)
    } catch (error) {
      this.error = error
      console.error(error)
    }
  },
}
</script>
