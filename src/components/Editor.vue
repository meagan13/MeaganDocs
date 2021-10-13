<template>
  <div class='m-5'>
    <div v-if="editor">
      <button class="btn" @click="editor.chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }">
        bold
      </button>
      <button class="btn" @click="editor.chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }">
        italic
      </button>
      <button class="btn" @click="editor.chain().focus().toggleStrike().run()" :class="{ 'is-active': editor.isActive('strike') }">
        strike
      </button>
      <button class="btn" @click="editor.chain().focus().toggleCode().run()" :class="{ 'is-active': editor.isActive('code') }">
        code
      </button>
      <button class="btn" @click="editor.chain().focus().unsetAllMarks().run()">
        clear marks
      </button>
      <button class="btn" @click="editor.chain().focus().toggleCodeBlock().run()" :class="{ 'is-active': editor.isActive('codeBlock') }">
        code block
      </button>
      <button class="btn" @click="editor.chain().focus().toggleBlockquote().run()" :class="{ 'is-active': editor.isActive('blockquote') }">
        blockquote
      </button>
      <button class="btn" @click="editor.chain().focus().setHorizontalRule().run()">
        horizontal rule
      </button>
      <button class="btn" @click="editor.chain().focus().setHardBreak().run()">
        hard break
      </button>
      <button class="btn" @click="editor.chain().focus().undo().run()">
        undo
      </button>
      <button class="btn" @click="editor.chain().focus().redo().run()">
        redo
      </button>
    </div>

    <div class="h-screen bg-pink-700 text-gray-800 italic m-2 p-2 rounded" >
      <editor-content class="bg-green-200 h-full p-2 rounded" :editor="editor" />
    </div>

  </div>
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

export default {
  components: {
    EditorContent,
  },

  data() {
    return {
      editor: null,
    }
  },

  mounted() {
    this.editor = new Editor({
      extensions: [
        StarterKit,
      ],
      content: `
        <p class="text-green-500">Begin editing here</p>
      `,
    })
  },

  beforeUnmount() {
    this.editor.destroy()
  },
}
</script>

// <style lang="scss">
// /* Basic editor styles */
// .ProseMirror {
//   > * + * {
//     margin-top: 0.75em;
//   }

//   ul,
//   ol {
//     padding: 0 1rem;
//     display: list-item;
//   }

//   h1,
//   h2,
//   h3,
//   h4,
//   h5,
//   h6 {
//     line-height: 1.1;
//   }

//   code {
//     background-color: rgba(#616161, 0.1);
//     color: #616161;
//   }

//   pre {
//     background: #0D0D0D;
//     color: #FFF;
//     font-family: 'JetBrainsMono', monospace;
//     padding: 0.75rem 1rem;
//     border-radius: 0.5rem;

//     code {
//       color: inherit;
//       padding: 0;
//       background: none;
//       font-size: 0.8rem;
//     }
//   }

//   img {
//     max-width: 100%;
//     height: auto;
//   }

//   blockquote {
//     padding-left: 1rem;
//     border-left: 2px solid rgba(#0D0D0D, 0.1);
//   }

//   hr {
//     border: none;
//     border-top: 2px solid rgba(#0D0D0D, 0.1);
//     margin: 2rem 0;
//   }
// }
// </style>
