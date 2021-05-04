<template>
  <div class="container">
    <div class="m-1 p-1">
      <h1>Add Tax</h1>
      <Form class="form-group">
        <div class="form-inline">
          <input
            id="wordPercentage"
            type="text"
            class="form-control m-1"
            placeholder="percentage in word"
            name="wordPercentage"
            style="width: 500px"
          />
          <span class="wrapper">
            <input
              id="numPercentage"
              class="form-control m-1"
              type="number"
              name="numPercentage"
              placeholder="percentage"
            />
          </span>
        </div>
        <p class="m-1 p-1">
          <input
            id="all"
            type="radio"
            class="m-1 p-1"
            name="all"
            :checked="selectedAll"
            @change="updateStatus($event)"
            @click="selectedAll = !selectedAll"
          />Apply to all items in collection
        </p>
        <p class="m-1 p-1">
          <input
            id="some"
            class="m-1 p-1"
            type="radio"
            name="some"
            :checked="selectedSome"
            @change="updateStatus($event)"
            @click="selectedSome = !selectedSome"
          />
          Apply to specific item
        </p>
        <hr />
        <div>
          <span class="searchItem form-inline">
            <input
              id="search"
              placeholder="search items"
              class="form-control p-1 m-1"
              style="width: 400px"
              type="text"
              name="search"
            />
          </span>
          <p
            v-for="item in items"
            :key="item.id"
            :class="item.id === 14864 || item.id === 14868 ? 'item-cat' : 'm-2'"
          >
            <input
              :id="item.id"
              type="checkbox"
              :value="item.id"
              :checked="checkedAll"
              @input="getinfo(item.id, $event)"
            />
            <label :for="item.id"> {{ item.name }}</label>
          </p>
        </div>
        <button class="btn btn-primary float-right mb-2 mt-0">
          Add Tax to {{ count }} items
        </button>
      </Form>
    </div>
  </div>
</template>

<script>
import data from '../pages/apidata.json'
export default {
  data() {
    return {
      selectedAll: false,
      selectedSome: false,
      checkedAll: false,
      count: 0,
      items: data,
    }
  },
  methods: {
    updateStatus(e) {
      if (e.target.id === 'all') {
        this.checkedAll = true
        this.selectedSome = false
        this.count = 6
      } else if (e.target.id === 'some') {
        this.checkedAll = false
        this.selectedAll = false
      }
      // if (e.target.id === '') {
      //   // eslint-disable-next-line no-console
      //   console.log(this.selectedAll)
      // }
    },
    getinfo(v, e) {
      if (e.target.checked) {
        this.count = this.count + 1
        // eslint-disable-next-line no-console
        console.log(this.count)
      }
    },
  },
}
</script>

<style>
/* .container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
} */
.wrapper input[type='text'] {
  position: relative;
}

.wrapper::after {
  position: relative;
  left: -45px;
  content: '%';
}
.searchItem input[type='text'] {
  position: relative;
}

.item-cat {
  background: rgb(201, 198, 198);
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', 'FontAwesome', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
