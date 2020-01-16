<template>
  <section class="section">
    <div class="container">
      <div class="columns is-multiline">
        <div class="column is-one-quarter" v-for="(article, index) in articles" :key="index">
          <a :href="article.url" target="_blank">
            <div class="card">
              <div class="card-image">
                <figure class="image is-3by2">
                  <img :src="article.urlToImage" :alt="article.title" />
                </figure>
              </div>
              <div class="card-content">
                <div class="content">
                  <p><span class="tag is-medium">{{ article.source.name }}</span></p>
                  <p class="title is-4">{{ article.title }}</p>
                  <p>{{ article.description }}</p>
                </div>
              </div>
            </div>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  async asyncData({ app }) {
    const { articles } = await app.$axios.$get(
      `https://newsapi.org/v2/everything?q=bitcoin&sortBy=publishedAt&apiKey=${process.env.API_KEY}`
    );

    return { articles };
  }
};
</script>
