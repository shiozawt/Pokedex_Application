<template>
<div class="home">
<h4>Finally, a website where you can upload all the pokemon you've caught into your
very own Pokedex. To add a new Pokemon you've caught, click the 'Edit Pokemon List' button.
To return home, click on the black Pokeball icon. Have fun!</h4>
<hr>
  <section class="image-gallery">
    <div class="image" v-for="item in items" :key="item.id">
      <img :src="item.path" />
      <center>
      <h2>{{item.title}} (#{{item.pokedexNumber}})</h2>
      </center>
    </div>
  </section>
</div>

</template>

<script>
// @ is an alias to /src

import axios from 'axios';

export default {
  name: 'Home',
  data() {
  return {
   items: [],
  }
},
created() {
  this.getItems();
},
methods: {
  async getItems() {
    try {
      let response = await axios.get("/api/items");
      this.items = response.data;
      return true;
    } catch (error) {
      console.log(error);
    }
  },
}

}
</script>

<style scoped>
.image h2 {
  font-style: italic;
}

/* Masonry */
*,
*:before,
*:after {
  box-sizing: inherit;
}

.image-gallery {
  column-gap: 1.5em;
}

.image {
  margin: 0 0 1.5em;
  display: inline-block;
  width: 100%;
}

.image img {
  width: 100%;
}

/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .image-gallery {
    column-count: 4;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image-gallery {
    column-count: 3;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .image-gallery {
    column-count: 2;
  }
}
</style>

<script>
import axios from 'axios';

export default {
  name: 'Admin',
  data() {
  return {
  findTitle: "",
  findItem: null,
  items: [],
    title: "",
    pokedexNumber: "",
    file: null,
    addItem: null,
  }
  },
  computed: {
  suggestions() {
    let items = this.items.filter(item => item.title.toLowerCase().startsWith(this.findTitle.toLowerCase()));
    return items.sort((a, b) => a.title > b.title);
  }
  },
  created() {
  this.getItems();
  },
  methods: {
  fileChanged(event) {
    this.file = event.target.files[0]
  },
  async upload() {
  try {
    const formData = new FormData();
    formData.append('photo', this.file, this.file.name)
    let r1 = await axios.post('/api/photos', formData);
    let r2 = await axios.post('/api/items', {
      title: this.title,
      pokedexNumber: this.pokedexNumber,
      path: r1.data.path
    });
    this.addItem = r2.data;
  } catch (error) {
    console.log(error);
  }
  },
  async getItems() {
  try {
    let response = await axios.get("/api/items");
    this.items = response.data;
    return true;
  } catch (error) {
    console.log(error);
  }
},
async editItem(item) {
  try {
    await axios.put("/api/items/" + item._id, {
      title: this.findItem.title,
    });
    this.findItem = null;
    this.getItems();
    return true;
  } catch (error) {
    console.log(error);
  }
},
selectItem(item) {
  this.findTitle = "";
  this.findItem = item;
},
async deleteItem(item) {
  try {
    await axios.delete("/api/items/" + item._id);
    this.findItem = null;
    this.getItems();
    return true;
  } catch (error) {
    console.log(error);
  }
}
}

}
</script>
