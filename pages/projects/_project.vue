<template>
  <main>
    <section v-if="post">
      <nav class="mb-8" aria-label="go back">
        <router-back class="block" />
      </nav>
      <!-- <div class="box">hello</div> -->

      <article class="box">
        <img v-if="post.cover" class="cover-image" :src="post.cover" />
        <!-- <h6 class="inline py-1 px-2 mr-1 bg-gray text-white text-sm font-medium rounded-sm">{{ post.category }}</h6> -->
        <h1 class="">{{ post.title }}</h1>
        <p class="mt-1 mb-8 text-primary-600 dark:text-primary-400">{{ post.description }}</p>
        <nuxt-content :document="post" />
        <div v-if="post.gallery" class="nuxt-content">
          <img v-for="image in post.gallery" class="image" :key="image.id" :src="image" />
        </div>
      </article>
    </section>
  </main>
</template>

<script>
import gsap from 'gsap'
export default {
  async asyncData({ $content, params, error }) {
    let post
    try {
      post = await $content('projects', params.project).fetch()
    } catch (e) {
      error({ message: 'Project not found' })
    }
    return { post }
  },
  mounted() {
    // const { box } = this.$refs
    // const timeline = gsap.timeline();

    // gsap.to(box, 1, { x: 200, rotation: 90 })
    // gsap.to('.box', { duration: 2, x: 100 })
    gsap.fromTo(
      '.box',
      { duration: 1, ease: 'elastic. out( 1, 0.3)', y: -100 },
      { duration: 1, ease: 'elastic. out( 1, 0.3)', y: 0 }
    )
  },
}
</script>
<style scoped>
.box {
  /* height: 100px;
  width: 100px; */
  height: 100%;
  width: 100%;
  background: darkolivegreen;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  flex-flow: column wrap;
  /* color: black; */
  padding: 20px;
}
</style>
