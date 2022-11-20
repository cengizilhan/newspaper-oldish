import
<template>
  <div class="home">
    <div class="head">
            <div class="headerobjectswrapper">
                <div class="weatherforcastbox"><span style="font-style: italic;">Weatherforcast for the next 24 hours:
                        Plenty of Sunshine</span><br><span>Wind: 7km/h SSE; Ther: 21°C; Hum: 82%</span></div>
                <header>Son Havadis</header>
            </div>

            <div class="subhead">York, MA - Thursday August 30, 1978 - Seven Pages</div>
        </div>
        <div class="content" v-if="fetchedItems">
          <div class="collumns" >
               <News  :news="item"  v-for="item in fetchedItems" :key="item.id"></News>
            </div>
        </div>
  </div>
</template>

<script>
import News from '../components/News.vue'
export default {
  name: 'HomeView',
  components: {
    News
  },
  created () {
    this.items = localStorage.getItem('items') ? JSON.parse(localStorage.getItem('items')) : []
    // GET request using fetch with set headers
    const headers = { 'Content-Type': 'application/json', Authorization: 'apikey 6PNFHS0yEd3MvykSxBBkEb:11WKdNSKTh6TP6rOiuozYB' }
    fetch('https://api.collectapi.com/news/getNews?country=tr&tag=sport', { headers })
      .then(response => response.json())
      .then(data => (this.fetchedItems = data.result))
  },
  data () {
    return {
      newItem: '',
      items: [{
        msg: 'msg test',
        id: 2,
        description: 'descrip text',
        image: 'img test',
        title: 'title text',
        source: 'sourcee',
        date: 'date'
      }
      ],
      fetchedItems: []
    }
  },
  watch: {
    items: {
      handler (items) {
        localStorage.setItem('items', JSON.stringify(this.items))
      },
      deep: true
    }
  },
  methods: {
    addItem () {
      if (this.newItem) {
        this.items.push({
          id: this.items.length + 1,
          name: this.newItem,
          completed: false
        })
        this.newItem = ''
      }
    },
    toggleItemCompletion (item) {
      item.completed = !item.completed
    },
    removeItem (item) {
      this.items.splice(this.items.indexOf(item), 1)
    },
    updateName (item, index) {
      this.items[index].name = item.name
    },
    editItem (item, index) {
      this.items[index].name = prompt('Edit item', item.name)
    }
  }
}
</script>
<style>
.checked{
  text-decoration: line-through;
}
</style>
