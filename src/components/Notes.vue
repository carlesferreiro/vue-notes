<template>
  <div>
    <ul>
      <li v-for="note in notes">
        <button @click="remove(note.id)">&times;</button>
        {{ note.description }}
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    name: 'Notes',
    props: {
      notes: Array
    },
    methods: {
     remove(id) {
      this.$emit('remove', id);
    }
  }
}
</script>

<style scoped lang="scss">
ul {
  list-style-type: none;
  padding: 0;

  li {
    position: relative;
    display: inline-block;
    width: 200px;
    padding: 1em 1.5em;
    margin: 0.5em;
    color: #333;
    background: #fff684;
    overflow: hidden;
    border-left: 1px solid #ddd;
    border-bottom: 1px solid #ddd;

    &::before {
      content: "";
      position: absolute;
      top: 0;
      right: 0;
      border-width: 0 16px 16px 0;
      border-style: solid;
      border-color: #fff #fff #d6cd2f #d6cd2f;
      background: #d6cd2f;
      box-shadow: 0 1px 1px rgba(0,0,0,0.1), -1px 1px 1px rgba(0,0,0,0.1);
    }

    button {
      position: absolute;
      right: 10px;
      bottom: 10px;
      background: transparent;
      border: 0px;
      font-weight: bold;
      font-size: 20px;
      line-height: 1em;
      padding: 0px;
      margin: 0px;
      cursor: pointer;
    }
  }
}
</style>
