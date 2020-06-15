<template>
  <div class="toolbar">
    <a href="javascript:void(0)" @click="$emit('change-style', 'bold')">
      <span class="fa fa-bold fa-fw"></span>
    </a>
    <a href="javascript:void(0)" @click="$emit('change-style', 'italic')">
      <span class="fa fa-italic fa-fw"></span>
    </a>
    <a href="javascript:void(0)" @click="$emit('change-style', 'underline')">
      <span class="fa fa-underline fa-fw"></span>
    </a>
    <label for="change-font-size">Font Size: </label>
    <select
      style="margin-right: 5px;"
      v-model="selected"
      @change="$emit('change-style', 'fontSize', selected + 'px')"
    >
      <option
        v-for="fontSize in fontSizes"
        :key="fontSize.text"
        v-bind:value="fontSize.value"
        :selected="fontSize.value===3 ? true : false"
      >{{ fontSize.text }}</option>
    </select>
    <label for="change-font-color">Font Color: </label>
    <input
      value="#ffffff"
      type="color"
      @change="$emit('change-style', 'foreColor', $event.target.value)"
    />

    <label for="change-font-background">Font Background: </label>
    <input
      value="#ffffff"
      type="color"
      @change="$emit('change-style', 'backColor', $event.target.value)"
    />
    <button @click="$emit('log')">Log JSON</button>
  </div>
</template>

<script>
export default {
  name: "Toolbar",
  data() {
    return {
      selected: 3,
      fontSizes: [
        { value: 1, text: "Small" },
        { value: 3, text: "Normal" },
        { value: 5, text: "Large" },
        { value: 7, text: "Huge" }
      ]
    };
  }
};
</script>

<style>
.toolbar {
  min-height: 40px;
  width: 60%;
  border: solid 1px #ddd;
  background: #f4f4f4;
  padding: 5px;
  border-radius: 3px;
}

.toolbar a {
  color: black;
  margin-right: 5px;
}

.toolbar a:hover {
  color: #777;
}

.toolbar input, select {
  margin-right: 5px;
}

.toolbar button {
  padding: 0 5px;
}
</style>
