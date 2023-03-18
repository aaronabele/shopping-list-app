<template>
  <div class="shopping-list-styling">
    <div class="header">
      <img src="@/assets/shops.png" alt="pic" />
      <h1>{{ msg }}</h1>
      <button v-if="editing" @click="doEdit()" class="button-cancel-styling">
        Cancel
      </button>
      <button v-else @click="doEdit()" class="button-submit-styling">
        Add Item
      </button>
    </div>
    <div class="section-active-deactive-form-styling"></div>
    <div v-if="editing === true">
      <input
        class="input-field-styling"
        v-model="newItem"
        type="text"
        placeholder="Add your item here"
      />
      <button
        class="button-submit-styling"
        @click="addANewItem()"
        :disabled="newItem.length === 0"
      >
        Submit new item
      </button>
      <button class="button-remove-styling" @click="removePurchasedItem()">
        Remove purchased item
      </button>
      <br />
      <h2>{{ itemsHeader }}</h2>
      <p v-if="items.length === 0">Greate Job, you purchased all items</p>
      <ul v-else class="unordered-list-styling">
        <li
          v-for="item in items"
          :key="item.id"
          :class="[item.purchased ? 'text-gray' : '']"
        >
          <input
            type="checkbox"
            :checked="item.purchased"
            @click="togglePurchase(item)"
          />
          {{ item.label }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "ListComponent",
  props: {
    msg: String,
  },
  data() {
    return {
      itemsHeader: "List of Items to shop",
      editing: true,
      items: [
        { id: 1, label: "10 party hats", purchased: true },
        { id: 2, label: "2 board games", purchased: true },
        { id: 3, label: "20 cups", purchased: false },
      ],
      newItem: "",
      itemPurchased: false,
    };
  },
  methods: {
    addANewItem() {
      if (this.newItem.length != 0) {
        this.items.push({ id: this.items.length + 1, label: this.newItem });
        this.newItem = "";
      } else {
        alert("Please enter an Item, which is longer than 0 characters");
      }
    },
    doEdit() {
      this.editing = !this.editing;
      this.newItem = "";
    },
    togglePurchase(item) {
      return (item.purchased = !item.purchased);
    },
    removePurchasedItem() {
      const filteredItems = this.items.filter(
        (item) => item.purchased === false
      );
      return (this.items = filteredItems);
    },
  },
};
</script>

<style scoped>
.header {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1.2rem;
}

.section-active-deactive-form-styling {
  padding: 1rem;
}

ul {
  margin-top: 2rem;
  list-style-type: none;
  width: 100%;
}

li {
  display: flex;
  justify-content: center;
  align-items: center;
}

.shopping-list-styling {
  width: 50rem;
  height: 30rem;
  padding: 1rem;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
  background-color: white;
  border-radius: 15px;
}

.unordered-list-styling {
  font-size: 1.2rem;
}

.input-field-styling {
  width: 40%;
  height: 1.9rem;
  border-radius: 15px;
  border: 2px solid black;
  padding: 0.5rem;
}

.button-submit-styling {
  background-color: rgb(48, 160, 48);
  color: white;
  padding: 0.4rem;
  border-radius: 1rem;
  border: 1px solid rgb(48, 160, 48);
  margin-left: 1rem;
  cursor: pointer;
}
.button-cancel-styling {
  background-color: rgb(196, 40, 40);
  color: white;
  padding: 0.4rem;
  border-radius: 1rem;
  border: 1px solid rgb(196, 40, 40);
  margin-left: 1rem;
  cursor: pointer;
}

.button-remove-styling {
  background-color: rgb(173, 40, 196);
  color: white;
  padding: 0.4rem;
  border-radius: 1rem;
  border: 1px solid rgb(173, 40, 196);
  margin-left: 1rem;
  cursor: pointer;
}

.text-gray {
  color: gray;
}
</style>
