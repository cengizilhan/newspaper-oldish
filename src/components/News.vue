<template>
  <div class="collumn">
    <div class="head">
      <span class="headline hl1">{{news.name}}</span>
      <p>
        <span class="headline hl2"
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
        "This time, let go your conscious self and act on instinct."
      </figcaption>
    </figure>
    <p>
      Leave that to me. Send a distress signal, and inform the Senate that all
      on board were killed
      <span class="citation"
        >"Don't under&shy;estimate the Force. I suggest you try it again,
        Luke."</span
      >
      This time, let go your conscious self and act on instinct. In my
      experience, there is no such thing as luck. You're all clear, kid. Let's
      blow this thing and go home!
    </p>
    <p>
      You don't believe in the Force, do you? Partially, but it also obeys your
      commands. The plans you refer to will soon be back in our hands. As you
      wish.
    </p>
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
