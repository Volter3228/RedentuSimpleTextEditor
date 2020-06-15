<template>
  <div class="wrapper">
    <h1>GREETINGS, BEST MAN (OR WOMAN) FROM REDENTU TEAM!</h1>
    <br />
    <Toolbar v-on:change-style="changeTextStyle" v-on:log="logJSON" />
    <div
      class="editor"
      ref="textarea"
      contenteditable="true"
      @keydown.13="onReturn"
      spellcheck="false"
    ></div>
    <footer>Made by Vova Morozov, just a guy who wants to work hard with Redentu team</footer>
  </div>
</template>

<script>
import Toolbar from "./Toolbar";

export default {
  name: "TextEditor",
  components: {
    Toolbar
  },
  data() {
    return {};
  },
  methods: {
    onReturn: function(e) {
      e.preventDefault();
      document.execCommand("insertHTML", false, "<br>\u200C");
      return false;
    },
    changeTextStyle: function(command, value) {
      document.execCommand("styleWithCSS", false, true);
      document.execCommand(command, false, value);
      this.unwrapNested();
    },
    logJSON: function() {
      let json = {
        textNodes: []
      };
      let childNodes = this.$refs.textarea.childNodes;
      childNodes.forEach(child => {
        if (child.nodeName === "#text") {
          json.textNodes.push({
            text: child.nodeValue,
            color: "#000",
            backColor: "#fff",
            fontSize: "14px"
          });
        } else {
          json.textNodes.push({
            text: child.textContent,
            color: child.style.color ? child.style.color : "#000",
            backColor: child.style.backgroundColor
              ? child.style.backgroundColor
              : "#fff",
            fontSize: child.style.fontSize ? child.style.fontSize : "14px"
          });
        }
      });
      console.log(json);
    },
    unwrapNested: function() {
      let children = this.$refs.textarea.children;
      let counter = 0;
      children.forEach(parent => {
        if (parent.children.length) {
          counter = 0;
          parent.childNodes.forEach(child => {
            if (child.nodeName === "#text") {
              let wrapper = document.createElement("span");
              wrapper.style.cssText = parent.style.cssText;
              wrapper.textContent = child.textContent;
              parent.insertBefore(wrapper, parent.childNodes[counter]);
              child.remove();
            } else {
              child.style.cssText = child.style.cssText + parent.style.cssText;
            }
            counter++;
          });
          parent.outerHTML = parent.innerHTML;
        }
      });
    }
  }
};
</script>

<style>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 40px;
}
.wrapper h1 {
  color: deepskyblue;
}
.wrapper footer {
  color: gray;
  font-size: 12px;
  font-style: italic;
}
.editor {
  width: 60%;
  min-height: 420px;
  border: 1px solid #666;
  margin-bottom: 10px;
  padding: 10px 8px;
  overflow-x: scroll;
  overflow-y: hidden;
  white-space: nowrap;
  -webkit-overflow-scrolling: touch;
}

.editor span .editor:focus {
  border-color: #000;
}
</style>
