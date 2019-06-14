<template>
  <div>
    <!-- <b-dropdown id="dropdown-1"  text="Amount" class="m-md-2">
      <b-dropdown-item v-for="(category, index) in categories" :key="index">{{ category }}</b-dropdown-item>
    </b-dropdown> -->
    <b-form-input type="number" autocomplete="off" list="my-list-id" min="1" max="50" placeholder="Amount" class="config-panel-1"></b-form-input>
    <datalist autocomplete="off" id="my-list-id" >
      <option autocomplete="off" v-for="(amount, index) in amountChoices" :key="index">{{ amount }}</option>
    </datalist>
    
    <b-dropdown id="dropdown-category" offset="-121" text="Category" class="m-md-2 config-panel">
      <b-dropdown-item v-for="(category, index) in categories" :key="index">{{ category }}</b-dropdown-item>
    </b-dropdown>
    <b-dropdown id="dropdown-1" text="Difficulty" class="m-md-2 config-panel">
      <b-dropdown-item v-for="(difficult, index) in difficulty" :key="index">{{ difficult }}</b-dropdown-item>
    </b-dropdown>

  </div>
</template>

<script>
export default {
  props: {
    hello: String,
    categories: Array,
    difficulty: Array
  },
  data() {
    return {
      amountOfQuestions: [],
      amountChoices: [5, 10, 15, 20, 25, 30, 35, 40, 45, 50]
    }
  },
  methods: {
    toFifty() {
      let array = []
      for (let i = 1; i < 51; i++) {
        array.push(i)
      }
      this.amountOfQuestions = array
    }
  },
  mounted() {
    this.toFifty()
    console.log(this.amountOfQuestions)
  }
}
</script>

<style>
  .dropdown-menu {
    overflow-y: scroll;
    max-height: 220px;
  }

.dropdown-menu::-webkit-scrollbar {
    width: 0 !important;
}
.dropdown-menu {
    overflow-y: scroll;
    scrollbar-width: none; /* Firefox */
    -ms-overflow-style: none;  /* IE 10+ */
}

.config-panel-1 {
  margin: 30px 10px 0 0;
}

.form-control {
  width: 122px;
  display: inline-block;
}

@media only screen and (max-width: 768px) {
  .config-panel-1 {
    margin: 30px 0 0 0;
  }
  .config-panel {
    margin-left: 15px 
  }
}
</style>
