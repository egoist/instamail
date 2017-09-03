<template>
  <form class="form" @submit.prevent="handleSubmit">
    <div class="form-meta">
      <div class="group">
        <input
          class="control"
          placeholder="Subject"
          v-model="subject"
        >
      </div>
      <div class="group">
        <input
          type="email"
          class="control"
          placeholder="From"
          v-model="from"
        >
      </div>
      <div class="group">
        <input
          type="email"
          class="control"
          placeholder="To"
          v-model="to"
        >
      </div>
    </div>
    <div class="form-content">
      <monaco-editor
        ref="monaco"
        style="height: 100%;width:100%;"
        placeholder="content"
        language="markdown"
        v-model="content"
        :options="editorOptions"
        @editorMount="handleEditorMount"
        placeholder="Loading editor..."
      />
    </div>
    <div class="form-action">
      <button
        class="button primary"
        type="submit">
        {{ sending ? 'Sending' : 'Send' }}
      </button>
      <div class="right">
        <a href="https://github.com/egoist/instamail">source code</a>
      </div>
    </div>
  </form>
</template>

<script>
import marked from 'marked3'
import toast from 'native-toast'
import axios from 'axios'

import MonacoEditor from 'vue-monaco'

export default {
  data() {
    return {
      from: '',
      to: '',
      subject: '',
      content: 'Send email anonymously...\n\npifff, it supports markdown too!',
      sending: false,
      editorOptions: {
        lineNumbers: false,
        minimap: {
          enabled: false
        }
      }
    }
  },

  methods: {
    async handleSubmit() {
      this.sending = true
      try {
        await axios.post('https://send-mail.egoist.moe/send', {
          from: this.from,
          to: this.to,
          subject: this.subject,
          html: marked(this.content)
        })
        toast({
          type: 'success',
          message: 'Success'
        })
      } catch (err) {
        if (err.response) {
          toast({
            type: 'error',
            message: err.response.data.message
          })
        } else {
          toast({
            type: 'error',
            message: err.message
          })
        }
      }
      this.sending = false
    },

    handleEditorMount(e) {
      e.model.updateOptions({
        tabSize: 2
      })
      e.focus()
    }
  },

  components: {
    MonacoEditor
  }
}
</script>

<style src="native-toast/dist/native-toast.css"></style>

<style scoped>
.form {
  height: 100%;
}

.form-meta {
  display: flex;
  height: 40px;
}

.form-content {
  height: calc(100% - 40px - 40px);
}

.form-content .control {
  height: 100%;
}

.form-action {
  height: 40px;
  padding: 0 10px;
  display: flex;
  align-items: center;
  border-top: 1px solid #e2e2e2;
  justify-content: space-between;
}

.form-meta .group {
  width: 33.3333%;
}

.form-meta .group .control {
  width: 100%;
  padding: 10px;
}

.form-meta .group:not(:last-child) .control {
  border-right: 1px solid #e2e2e2;
}

.form-meta .group .control:focus {
  background: #f9f9f9;
}

.control {
  outline: none;
  padding: 5px 0;
  border: none;
  border-bottom: 1px solid #e2e2e2;
  width: 240px;
  font-size: 1rem;
  background: transparent;
}

textarea.control {
  width: 100%;
  resize: none;
  padding: 10px;
}
</style>
