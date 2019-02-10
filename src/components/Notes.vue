<template>
  <div>
    <ul>
      <li :class="note.background" v-for="note in notes" v-bind:key="note.id">
        <!-- <button class="toggleedit" @click="toggleedit(note.id)">&#8634;</button> -->
        <button class="remove" @click="remove(note.id)">&times;</button>
        
        <textarea @blur="toggleedit(note.id)" class="textarea" v-if="note.editing" v-model="note.description"></textarea>
        <div @click="toggleedit(note.id)" v-else>{{ note.description }}</div>
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
    },
     toggleedit(id) {
      this.$emit('toggleedit', id);
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
    height: 200px;
    padding: 1em 1.5em;
    margin: 0.5em;
    color: #333;
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

      &.toggleedit {
        right: 30px;
      }
    }

    textarea {
      height: calc(100% - 20px);
      width: 100%;
      opacity: 0.8;
      resize: none;
    }

    &.yellow {
      background: #fdf7b7;

      &::before {
        border-color: #fff #fff #fdf7b7 #fdf7b7;
      }
    }

    &.blue {
      background: #8bcdec;

      &::before {
        border-color: #fff #fff #8bcdec #8bcdec;
      }
    }

    &.pink {
      background: #edc4c8;

      &::before {
        border-color: #fff #fff #edc4c8 #edc4c8;
      }
    }
  }
}
</style>
