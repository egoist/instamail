<template>
  <div id="app">
    <div class="main">
      <im-form />
    </div>
  </div>
</template>

<script>
import Form from '@/components/Form.vue'

export default {
  components: {
    'im-form': Form
  }
}
</script>

<style>
html, body, #app, .page, .sidebar, .main {
  height: 100%;
}

body {
  font: 14px/1.4 -apple-system,BlinkMacSystemFont,"Segoe UI","Roboto", "Oxygen","Ubuntu","Cantarell","Fira Sans","Droid Sans", "Helvetica Neue",sans-serif;
  background: #f0f0f0;
  margin: 0;
}

* {
  box-sizing: border-box;
}

.CodeMirror {
  height: 100% !important;
}

.main {
  max-width: 600px;
  margin: 0 auto;
  border-left: 1px solid #e2e2e2;
  border-right: 1px solid #e2e2e2;
  background: white;
}

.button {
  user-select: none;
  background: none;
  border: 1px solid transparent;
  border-radius: 0.3em;
  cursor: pointer;
  display: inline-block;
  font-weight: 500;
  line-height: 2.3em;
  height: 2.4em;
  margin-bottom: 0;
  overflow: hidden;
  padding: 0 1em;
  text-align: center;
  touch-action: manipulation;
  vertical-align: middle;
  white-space: nowrap;
  -webkit-appearance: none;
}

.button.primary {
  background-image: linear-gradient(to bottom, #2591ed 0%, #1177cd 100%);
  background-repeat: repeat-x;
  background-color: #1385e5;
  border-color: #1177cd #0f6ab6 #0d5c9e;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.1);
  color: white;
  font-weight: 400;
  text-shadow: 0 -1px 0 rgba(0, 0, 0, 0.25);
}
</style>


