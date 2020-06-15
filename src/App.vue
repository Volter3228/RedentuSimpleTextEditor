<template>
  <div id="app">
    <TextEditor />
  </div>
</template>

<script>
import TextEditor from './components/TextEditor/TextEditor';

export default {
  name: 'App',
  components: {
    TextEditor
  },
}
</script>

<style>

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

</style>
