<template>
<div class='bg-gray-100 invisible lg:visible lg:grid lg:grid-rows-2 lg:place-items-center lg:h-screen'>
    <div class='invisible lg:visible mx-5 bg-gray-300 h-screen w-4/5 p-2 lg:grid lg:grid-rows-5 lg:row-span-2'>
      <div v-if="editor">
        <div class='bg-red-300 visible lg:visible lg:grid lg:grid-flow-col'>
          <div >
            <button class="btn btn-large font-bold" title="Bold" @click="editor.chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }">
             B
            </button>

            <button class="btn btn-large italic" title="Italic" @click="editor.chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }">
              I
            </button>

            <button class="btn btn-large line-through" title="Strikethrough" @click="editor.chain().focus().toggleStrike().run()" :class="{ 'is-active': editor.isActive('strike') }">
              S
            </button>
<!--
            <button class="btn btn-large" @click="editor.chain().focus().toggleCode().run()" :class="{ 'is-active': editor.isActive('code') }">
              code
            </button> -->

            <button class="btn btn-large" @click="editor.chain().focus().unsetAllMarks().run()">
              <img class="w-6" src="../../images/clear-format.png" alt="clear formatting icon" title="Clear Formatting">
            </button>

            <button class="btn btn-large" title="Code Block" @click="editor.chain().focus().toggleCodeBlock().run()" :class="{ 'is-active': editor.isActive('codeBlock') }">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" />
              </svg>
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().toggleBlockquote().run()" :class="{ 'is-active': editor.isActive('blockquote') }">
              <img class="w-6" src="../../images/quote.png" alt="blockquote icon" title="Blockquote">
            </button>

            <button class="btn btn-large" title="Add Horizontal Line" @click="editor.chain().focus().setHorizontalRule().run()">
              <img class="w-6" src="../../images/line.png" alt="add line icon">
            </button>

            <button class="btn btn-large" title="Add Line Break" @click="editor.chain().focus().setHardBreak().run()">
              <img class="w-6" src="../../images/break.png" alt="line break icon">
            </button>

            <button class="btn btn-large" title="Undo" @click="editor.chain().focus().undo().run()">
              <img class="w-6" src="../../images/undo-arrow.png" alt="undo arrow icon">
            </button>

            <button class="btn btn-large" title="Redo" @click="editor.chain().focus().redo().run()">
              <img class="w-6" src="../../images/redo.png" alt="redo arrow icon">
            </button>
          </div>

          <div>
            <button class="btn btn-large inline table-add" @click="editor.chain().focus().insertTable({ rows: 3, cols: 3, withHeaderRow: true }).run()">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M3 14h18m-9-4v8m-7 0h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z" />
              </svg>

              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6" />
              </svg>
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().addColumnBefore().run()" :disabled="!editor.can().addColumnBefore()">
              <img class="w-6" src="../../images/add_column.svg">Before
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().addColumnAfter().run()" :disabled="!editor.can().addColumnAfter()">
              <img class="w-6" src="../../images/add_column.svg">After
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().deleteColumn().run()" :disabled="!editor.can().deleteColumn()">
              <img class="w-6" src="../../images/delete_column.svg">
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().addRowBefore().run()" :disabled="!editor.can().addRowBefore()">
              <img class="w-6" src="../../images/add_row.svg">Before
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().addRowAfter().run()" :disabled="!editor.can().addRowAfter()">
              <img class="w-6" src="../../images/add_row.svg">After
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().deleteRow().run()" :disabled="!editor.can().deleteRow()">
              <img class="w-6" src="../../images/delete_row.svg">
            </button>

            <button class="btn btn-large table-delete" @click="editor.chain().focus().deleteTable().run()" :disabled="!editor.can().deleteTable()">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 10h18M3 14h18m-9-4v8m-7 0h14a2 2 0 002-2V8a2 2 0 00-2-2H5a2 2 0 00-2 2v8a2 2 0 002 2z" />
              </svg>

              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16" />
              </svg>
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().mergeCells().run()" :disabled="!editor.can().mergeCells()">
              Merge Cells
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().splitCell().run()" :disabled="!editor.can().splitCell()">
              Split Cell
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().toggleHeaderColumn().run()" :disabled="!editor.can().toggleHeaderColumn()">
              Toggle Header Column
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().toggleHeaderRow().run()" :disabled="!editor.can().toggleHeaderRow()">
              Toggle Header Row
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().toggleHeaderCell().run()" :disabled="!editor.can().toggleHeaderCell()">
              Toggle Header Cell
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().mergeOrSplit().run()" :disabled="!editor.can().mergeOrSplit()">
              Merge Or Split
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().setCellAttribute('backgroundColor', '#FAF594').run()" :disabled="!editor.can().setCellAttribute('backgroundColor', '#FAF594')">
              Set Cell Attribute
            </button>

            <button class="btn btn-large" @click="editor.chain().focus().fixTables().run()" :disabled="!editor.can().fixTables()">
              Fix Tables
            </button>

            <button class="btn btn-large previous" @click="editor.chain().focus().goToNextCell().run()" :disabled="!editor.can().goToNextCell()">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
              </svg>
            </button>

            <button class="btn btn-large next" @click="editor.chain().focus().goToPreviousCell().run()" :disabled="!editor.can().goToPreviousCell()">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
              </svg>
            </button>

          </div>
        </div>
      </div>

      <div class="visible w-full overflow-auto row-start-3 row-end-6 justify-center bg-pink-700 text-gray-800 italic mt-2 p-2 rounded row-span-full editor-div" >
        <editor-content class="bg-green-200 w-full h-full p-2 rounded justify-center" :editor="editor" />
      </div>

    </div>

  </div>
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'
import Table from '@tiptap/extension-table'
import TableRow from '@tiptap/extension-table-row'
import TableCell from '@tiptap/extension-table-cell'
import TableHeader from '@tiptap/extension-table-header'

const CustomTableCell = TableCell.extend({
  addAttributes() {
    return {
      // extend the existing attributes …
      ...this.parent?.(),

      // and add a new one …
      backgroundColor: {
        default: null,
        parseHTML: element => element.getAttribute('data-background-color'),
        renderHTML: attributes => {
          return {
            'data-background-color': attributes.backgroundColor,
            style: `background-color: ${attributes.backgroundColor}`,
          }
        },
      },
    }
  },
})


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
        Table.configure({
          resizable: true,
        }),
        TableRow,
        TableHeader,
        // TableCell,
        CustomTableCell,
      ],
      content:'',
    })
  },

  beforeUnmount() {
    this.editor.destroy()
  },
}
</script>

<style lang="scss">
/* Basic editor styles */
.ProseMirror {
  margin: 1rem 0;

  > * + * {
    margin-top: 0.75em;
  }

  ul,
  ol {
    padding: 0 1rem;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    line-height: 1.1;
  }

  code {
    background-color: rgba(#616161, 0.1);
    color: #616161;
  }

  pre {
    background: #0D0D0D;
    color: #FFF;
    font-family: 'JetBrainsMono', monospace;
    padding: 0.75rem 1rem;
    border-radius: 0.5rem;

    code {
      color: inherit;
      padding: 0;
      background: none;
      font-size: 0.8rem;
    }
  }

  img {
    max-width: 100%;
    height: auto;
  }

  blockquote {
    padding-left: 1rem;
    border-left: 2px solid rgba(#0D0D0D, 0.1);
  }

  hr {
    border: none;
    border-top: 2px solid rgba(#0D0D0D, 0.1);
    margin: 2rem 0;
  }
}

/* Table-specific styling */
.ProseMirror {
  table {
    border-collapse: collapse;
    table-layout: fixed;
    width: 100%;
    margin: 0;
    overflow: hidden;

    td,
    th {
      min-width: 1em;
      border: 2px solid #ced4da;
      padding: 3px 5px;
      vertical-align: top;
      box-sizing: border-box;
      position: relative;

      > * {
        margin-bottom: 0;
      }
    }

    th {
      font-weight: bold;
      text-align: left;
      background-color: #f1f3f5;
    }

    .selectedCell:after {
      z-index: 2;
      position: absolute;
      content: "";
      left: 0; right: 0; top: 0; bottom: 0;
      background: rgba(200, 200, 255, 0.4);
      pointer-events: none;
    }

    .column-resize-handle {
      position: absolute;
      right: -2px;
      top: 0;
      bottom: -2px;
      width: 4px;
      background-color: #adf;
      pointer-events: none;
    }
  }
}

.tableWrapper {
  overflow-x: auto;
}

.resize-cursor {
  cursor: ew-resize;
  cursor: col-resize;
}
</style>
