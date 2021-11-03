<template>
<div class='bg-gray-100 h-screen w-screen justify-center p-0 mt-1'>
    <div v-if="editor" class="w-full">
      <div class='p-0 bg-gray-300 w-screen h-full place-content-center content-center justify-center'>
        <div class='bg-gray-300 p-2 flex flex-wrap place-content-center content-center justify-center'>
          <div class='md:bg-gray-400 flex content-center place-content-center w-11/12 max-w-3xl justify-center md:w-auto'>
            <button class="btn btn-large font-bold" title="Bold" @click="editor.chain().focus().toggleBold().run()" :class="{ 'is-active': editor.isActive('bold') }">
            <img class="w-6" src="../../images/bold.png" alt="bold icon" title="Bold">
            </button>

            <button class="btn btn-large italic" title="Italic" @click="editor.chain().focus().toggleItalic().run()" :class="{ 'is-active': editor.isActive('italic') }">
              <img class="w-6" src="../../images/italic-font.png" alt="italic icon">
            </button>

            <button class="btn btn-large line-through" title="Strikethrough" @click="editor.chain().focus().toggleStrike().run()" :class="{ 'is-active': editor.isActive('strike') }">
              <img class="w-6" src="../../images/strikethrough.png" alt="strikethrough icon">
            </button>

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
          </div>

          <div class="hidden invisible md:visible md:flex md:content-center">
            <img class="w-6 " src="../../images/vertical-line.png" alt="divider line icon">
          </div>

          <div class="md:bg-gray-400 flex content-center w-11/12 max-w-3xl md:w-auto justify-center">
            <button class="btn btn-large" title="Add Table" @click="editor.chain().focus().insertTable({ rows: 3, cols: 3, withHeaderRow: true }).run()">
              <img class="w-6" src="../../images/insert_table.png" alt="insert table icon">
            </button>

            <button class="btn btn-large" title="Add Column Left" @click="editor.chain().focus().addColumnBefore().run()" :disabled="!editor.can().addColumnBefore()">
              <img class="w-6" src="../../images/add_column_left.png" alt="add column before icon">
            </button>

            <button class="btn btn-large" title="Add Column Right" @click="editor.chain().focus().addColumnAfter().run()" :disabled="!editor.can().addColumnAfter()">
              <img class="w-6" src="../../images/add_column_right.png" alt="add column after icon">
            </button>

            <button class="btn btn-large" title="Delete Column" @click="editor.chain().focus().deleteColumn().run()" :disabled="!editor.can().deleteColumn()">
              <img class="w-6" src="../../images/delete_column.svg" alt="delete column icon">
            </button>

            <button class="btn btn-large" title="Add Row Above" @click="editor.chain().focus().addRowBefore().run()" :disabled="!editor.can().addRowBefore()">
              <img class="w-6" src="../../images/add_row_above.png" alt="add row above icon">
            </button>

            <button class="btn btn-large" title="Add Row Below" @click="editor.chain().focus().addRowAfter().run()" :disabled="!editor.can().addRowAfter()">
              <img class="w-6" src="../../images/add_row_below.png" alt="add row below icon">
            </button>

            <button class="btn btn-large" title="Delete Row" @click="editor.chain().focus().deleteRow().run()" :disabled="!editor.can().deleteRow()">
              <img class="w-6" src="../../images/delete_row.svg" alt="delete row icon">
            </button>

            <button class="btn btn-large table-delete" title="Delete Table" @click="editor.chain().focus().deleteTable().run()" :disabled="!editor.can().deleteTable()">
              <img class="w-6" src="../../images/delete_table.png" alt="delete table icon">
            </button>

            <button class="btn btn-large" title="Merge Cells" @click="editor.chain().focus().mergeCells().run()" :disabled="!editor.can().mergeCells()">
              <img class="w-6" src="../../images/merge.png" alt="merge cells icon">
            </button>

            <button class="btn btn-large" title="Split Cell" @click="editor.chain().focus().splitCell().run()" :disabled="!editor.can().splitCell()">
              <img class="w-6" src="../../images/split_cell.png" alt="split cell icon">
            </button>

            <button class="btn btn-large previous" title="Next Cell" @click="editor.chain().focus().goToNextCell().run()" :disabled="!editor.can().goToNextCell()">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
              </svg>
            </button>

            <button class="btn btn-large next" title="Previous Cell" @click="editor.chain().focus().goToPreviousCell().run()" :disabled="!editor.can().goToPreviousCell()">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 19l-7-7m0 0l7-7m-7 7h18" />
              </svg>
            </button>
          </div>

          <div class="hidden invisible md:visible md:flex md:content-center">
            <img class="w-6 " src="../../images/vertical-line.png" alt="divider line icon">
          </div>

          <div class="flex content-center">
            <button class="btn btn-large" title="Undo" @click="editor.chain().focus().undo().run()">
              <img class="w-6" src="../../images/undo_round.png" alt="undo arrow icon">
            </button>

            <button class="btn btn-large" title="Redo" @click="editor.chain().focus().redo().run()">
              <img class="w-6" src="../../images/redo.png" alt="redo arrow icon">
            </button>
          </div>

        </div>
      </div>
    </div>

    <div v-if="editor" class="bg-gray-200 p-5 md:grid grid-cols-12 h-screen">
      <div class="overflow-auto col-start-2 col-end-12 h-5/6 bg-green-800 text-gray-800 p-2 rounded" >
        <editor-content
          class="bg-gray-300 w-full h-full rounded justify-center"
          :editor="editor"
        />
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
  // margin: 1rem 0;

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

  min-height: 100%;
  max-height: 100%;
  overflow-y: scroll;
  padding: 1%;
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
