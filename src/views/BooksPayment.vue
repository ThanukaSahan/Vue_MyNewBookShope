<template>
  <div class="bodyDiv">
    <div class="detailDiv">
      <label>You have purchase following books</label>
      <ul>
        <li v-for="item in yourItems" :key="item.id">{{ item.bookname }}</li>
      </ul>
      <table>
        <tr v-for="book in yourItems" :key="book.id">
          <td class="col-sm col-1">
            <input
              type="checkbox"
              v-model="book.isItemSelected"
              @change="onSelectBook(book)"
            />
          </td>
          <td class="col-sm col-3">{{ book.bookname }}</td>
          <td class="col-sm col-3">{{ book.author }}</td>
          <td class="col-sm col-2">{{ book.category }}</td>
          <td class="col-sm col-2">{{ book.language }}</td>
          <td class="col-sm col-1">{{ book.price }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import { defineProps } from "vue";

export default {
  props: {
    yourItems: {
      type: Array,
      required: true,
    },
  },
  created() {
    const yourItemsJson = this.$route.query.yourItems;
    this.yourItems = JSON.parse(yourItemsJson);
  },
};
</script>

<style scoped>
.detailDiv {
  text-align: center;
  background-color: #fff;
  border: 1px dotted #c6bfbf;
}

.bodyDiv {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 30vh;
}
</style>