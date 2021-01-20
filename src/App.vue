<template>
  <div>
    <button @click="add()">Add an item</button>
    <table>
      <tr v-for="(item, index) in list" :key="index">
        <td>
          <form @submit.prevent="generate(index)">
            <span>What's your guess?</span>
            <select v-model="item.guess">
              <option disabled :value="undefined">Select one:</option>
              <option :value="true">Heads</option>
              <option :value="false">Tails</option>
            </select>
            <button v-if="item.reveal === false" type="submit"
              >Check</button>
            <span v-else-if="item.heads === item.guess"
              >Correct ({{ item.heads }})!</span>
            <span v-else>Alas, it's actually
            {{ item.heads === true ? 'Heads' : 'Tails' }}.</span>
          </form>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      list: [],
    };
  },
  methods: {
    add() {
      this.list.push({
        heads: undefined,
        guess: true,
        reveal: false,
      });
    },
    generate(index) {
      this.list[index].heads = true;
      this.list[index].reveal = true;
    },
  },
}
</script>
