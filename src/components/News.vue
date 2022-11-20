<template>
  <div class="collumn news-card">
    <div class="head">
      <span class="headline hl1">{{news.name}}</span>
      <p>
        <span class="headline hl2" style="display:none;"
          >Let go your conscious self and act on instinct</span
        >
      </p>
    </div>
    <p>
    {{news.description}}
    </p>
    <figure class="figure">
      <img class="media" :src=news.image alt="" />
      <figcaption class="figcaption">
        {{news.name}}
      </figcaption>
    </figure>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    news: {
      msg: String,
      id: Number,
      description: String,
      image: String,
      title: String,
      source: String,
      date: String
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only-->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
