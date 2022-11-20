import
<template>
  <div class="home">
    <div class="head">
            <div class="headerobjectswrapper">
                <div class="weatherforcastbox"><strong>Bugün 16 Sahife</strong></div>
                <header>Son Havadis</header>
            </div>

            <div class="subhead">Türkiye - {{date}}</div>
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
    document.title = 'Haberler'
    this.items = localStorage.getItem('items') ? JSON.parse(localStorage.getItem('items')) : []
    // GET request using fetch with set headers
    const headers = { 'Content-Type': 'application/json', Authorization: 'apikey 6PNFHS0yEd3MvykSxBBkEb:11WKdNSKTh6TP6rOiuozYB' }
    fetch('https://api.collectapi.com/news/getNews?country=tr&tag=general', { headers })
      .then(response => response.json())
      .then(data => (this.fetchedItems = data.result)).catch(error => {
        console.error('There was an error!', error)
        this.fetchedItems = this.errDummyItems
      })
    this.getDate()
  },
  data () {
    return {
      newItem: '',
      date: '',
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
      fetchedItems: [],
      errDummyItems: [
        {
          key: '0',
          url: 'https://www.hurriyet.com.tr/gundem/son-dakika-tokatta-ozel-hastanede-yogun-bakimda-skandal-bakan-koca-duyurdu-faaliyeti-durduruldu-42173949',
          description:
            'Tokat\'ta özel hastanede beyin kanaması nedeniyle tedavi gören Metin Akça\'ya (62) yoğun bakım ünitesinde 1\'i erkek 2 hemşirenin kötü muamelede bulunmasıyla ilgili Sağlık Bakanlığı\'nca soruşturma başlatılmıştı. Sağlık Bakanı Fahrettin Koca, soruşturma kapsamında hastanenin faaliyetinin durdurulduğunu açıkladı.',
          image:
            'https://i4.hurimg.com/i/hurriyet/75/620x350/637a315c4e3fe115103f5de1.jpg',
          name: 'Son dakika... Tokat\'ta özel hastanede yoğun bakımda skandal! Bakan Koca duyurdu: Faaliyeti durduruldu',
          source: 'Hürriyet',
          date: '2022-11-20T14:21:13.641Z'
        },
        {
          key: '1',
          url: 'https://www.hurriyet.com.tr/gundem/son-dakika-pence-kilic-harekatindan-yeni-goruntu-bombalara-yagmur-ve-ecrinin-adi-yazildi-42173961',
          description:
            'TSK\'nın Suriye ve Irak\'ın kuzeyine yönelik başlattığı Pençe Kılıç Hava Harekâtı kapsamında toplam 89 hedef imha edildi, çok sayıda terörist etkisiz hale getirildi. Milli Savunma Bakanlığı, harekâttan yeni bir görüntü paylaştı. Görüntülerde bombaların üzerine İstiklal Caddesi\'ndeki patlamada hayatını kaybeden Yağmur ve Ecrin\'in isimleri yazıldığı görülüyor.',
          image:
            'https://i4.hurimg.com/i/hurriyet/75/620x350/637a36344e3fe115103f5e47.jpg',
          name: 'Son dakika... Pençe Kılıç Harekâtı\'ndan yeni görüntü! Bombalara \'Yağmur\' ve \'Ecrin\'in adı yazıldı',
          source: 'Hürriyet',
          date: '2022-11-20T14:21:13.073Z'
        },
        {
          key: '2',
          url: 'https://www.cumhuriyet.com.tr/turkiye/teror-orgutu-pkk-suphelisi-yunanistana-kacarken-yakalandi-2004556',
          description: 'Terör örgütü PKK şüphelisi Yunanistan\'a kaçarken yakalandı.',
          image:
            'https://www.cumhuriyet.com.tr/Archive/2022/11/20/2004556/kapak_170151.jpg',
          name: 'Terör örgütü PKK şüphelisi Yunanistan\'a kaçarken yakalandı',
          source: 'Cumhuriyet',
          date: '2022-11-20T14:04:07.594Z'
        },
        {
          key: '3',
          url: 'https://www.karar.com/sehir-haberleri/hemzemin-gecitte-feci-kaza-coban-ve-30-koyun-oldu-1706457',
          description:
            'Kahramanmaraş\'ta, koyunlarıyla birlikte hemzemin geçitten karşıya geçmeye çalışan çobana yük treni çarptı. Feci olayda çoban ve 30 koyun hayatını kaybetti.',
          image: 'https://cdn.karar.com/news/1496625.jpg',
          name: 'Hemzemin geçitte feci kaza: Çoban ve 30 koyun öldü',
          source: 'KARAR',
          date: '2022-11-20T14:03:05.939Z'
        },
        {
          key: '4',
          url: 'https://www.karar.com/dunya-haberleri/uaea-baskani-grossi-zaporijya-nukleer-santralinde-art-arda-patlamalar-1706459',
          description:
            'Uluslararası Atom Enerjisi Ajansı Başkanı Grossi, dün akşamdan beri Zaporijya Nükleer Santrali çevresinden patlama sesleri geldiğini duyurdu. Grossi, olaya tepki göstererek \'Bunun arkasında kim varsa hemen durmalı. Daha önce de defalarca söylediğim gibi ateşle oynuyorsunuz\' çağrısında bulundu.',
          image: 'https://cdn.karar.com/news/1496626.jpg',
          name: 'UAEA Başkanı Grossi: Zaporijya Nükleer Santrali\'nde art arda patlamalar meydana geldi',
          source: 'KARAR',
          date: '2022-11-20T14:03:05.431Z'
        },
        {
          key: '5',
          url: 'https://www.karar.com/sehir-haberleri/anahtarini-evde-unutan-adamdan-tehlikeli-gosteri-cilingir-yerine-kepce-1706458',
          description:
            'Aydın\'da anahtarını evde unutan bir şahıs, çilingir çağırmak yerine sokaktaki beton dökme makinesini kullanan operatörden yardım istedi. Canını hiçe sayarak makinenin hortumuna tutunup evinin balkonuna giren şahıs, balkon kapısı kapalı olduğu için eylemini sonuçlandıramadı. Yaşanan ilginç anlar ise kameralara saniye saniye yansıdı.',
          image: 'https://cdn.karar.com/news/1496624.jpg',
          name: 'Anahtarını evde unutan adamdan tehlikeli gösteri! Çilingir yerine kepçe operatörü...',
          source: 'KARAR',
          date: '2022-11-20T14:03:04.895Z'
        },
        {
          key: '6',
          url: 'https://www.karar.com/hayat-haberleri/en-zeki-beyinleri-bile-zorlayan-optik-illuzyon-11-saniyede-resimdeki-1706460',
          description:
            'Bebeğin annesi bu eski tablodaki göz önünde saklanıyor. Bebeğin annesini 11 saniyede görebiliyorsan sen bir dahisin. Şimdi bu optik illüzyon mücadelesini deneyerek gözlem becerilerinizi test edin!',
          image: 'https://cdn.karar.com/news/1496627.jpg',
          name: 'En zeki beyinleri bile zorlayan optik illüzyon! 11 saniyede resimdeki bebeğin annesini bulabilir misin?',
          source: 'KARAR',
          date: '2022-11-20T14:03:04.377Z'
        },
        {
          key: '7',
          url: 'https://www.karar.com/dunya-haberleri/cop27de-anlasma-tamam-iklim-krizine-karsi-savunmasiz-ulkeler-icin-fon-1706461',
          description:
            'Mısır’da düzenlenen BM İklim Değişikliği Zirvesi (COP27) son buldu. Zirve sonunda alınan kararla gelişmiş ülkeler iklim değişikliği ile mücadelede yoksul ülkelere fon sağlama konusunda anlaştı.',
          image: 'https://cdn.karar.com/news/1496628.jpg',
          name: 'COP27\'de anlaşma tamam: İklim krizine karşı savunmasız ülkeler için fon kurulacak',
          source: 'KARAR',
          date: '2022-11-20T14:03:03.860Z'
        }
      ]

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
    getDate () {
      const options = {
        year: 'numeric',
        month: 'long',
        day: 'numeric'
      }
      this.date = new Date().toLocaleDateString('tr-TR', options)
    },
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
