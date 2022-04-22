<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  data() {
    return {
      hideTextEdit: true,
      hideTableEdit: true,
    }
  },
  methods: {
    toggleShowText() {
      // if(this.hideTableEdit = true) {
      //   this.hideTableEdit = !this.hideTableEdit;
      // }
      this.hideTextEdit = !this.hideTextEdit;
      console.log(this.hideTextEdit)

    },
    toggleShowTable() {
      // if(this.hideTextEdit = false) {
      //   this.hideTextEdit = !this.hideTextEdit;
      //   console.log("after switch function:", this.hideTextEdit)
      // }
      this.hideTableEdit = !this.hideTableEdit;
    }
  }
})
</script>

<template>
  <div @keyup.50="findName" class="bg-gray-200 h-screen w-screen justify-center p-0 mt-1">
    <!-- <button class='lg:hidden'
        @click="editor.chain().focus().insertTable({ rows: 3, cols: 3, withHeaderRow: true }).run()"
      >
        <img class="w-4 lg:w-6" src="../../images/insert_table.png" alt="insert table icon" />
    </button>-->

    <div>
      <editor-content :editor="editor" />
    </div>

    <div v-if="editor" class="bg-gray-200 p-5 lg:grid grid-cols-12 content-center">

      <div class="overflow-auto col-start-3 col-end-11 bg-gray-400 text-gray-800 p-2 rounded">
        <editor-content class="bg-gray-100 w-full h-full rounded justify-center" :editor="editor" />
      </div>

      <div class="flex justify-items-stretch col-start-10 col-end-11">
        <button @click="toggleShowText" class="p-2">
          <img src="../../images/text-format.png"/>
        </button>
      <!-- </div> -->

      <!-- <div class="col-start-10 col-end-11"> -->
        <button @click="toggleShowTable" class="h-1 p-2">
          <img src="../../images/edit-table.png" alt="edit table" class="w-6" />
        </button>
      </div>
    </div>

    <bubble-menu class="lg:hidden" :editor="editor" v-if="editor">
      <button
        @click="editor.chain().focus().toggleBold().run()"
        :class="[{ 'is-active': editor.isActive('bold') }, 'p-1 bg-gray-200 border border-gray-500']"
      >
        <img class="w-4 lg:w-6" src="../../images/bold.png" alt="bold icon" title="Bold" />
      </button>

      <button
        @click="editor.chain().focus().toggleItalic().run()"
        :class="[{ 'is-active': editor.isActive('italic') }, 'p-1 bg-gray-200 border border-gray-500']"
      >
        <img
          class="w-4 lg:w-6"
          src="../../images/italic-font.png"
          alt="italic icon"
          title="Italicsssssss"
        />
      </button>

      <button
        @click="editor.chain().focus().toggleStrike().run()"
        :class="[{ 'is-active': editor.isActive('strike') }, 'p-1 bg-gray-200 border border-gray-500']"
      >
        <img
          class="w-4 lg:w-6"
          src="../../images/strikethrough.png"
          alt="strikethrough icon"
          title="Strikethrough"
        />
      </button>

      <button
        @click="editor.chain().focus().unsetAllMarks().run()"
        :class="[{ 'is-active': editor.isActive('unset')}, 'p-1 bg-gray-200 border border-gray-500']"
      >
        <img
          class="w-4 lg:w-6"
          src="../../images/clear-format.png"
          alt="clear formatting icon"
          title="Clear Formatting"
        />
      </button>

    </bubble-menu>

    <div v-if="editor" class="w-full">
      <div
        class="p-0 bg-gray-200 w-screen h-full place-content-center content-center justify-center"
      >
        <div
          class="findme w-full bg-gray-200 lg:p-2 flex flex-wrap place-content-center items-center content-center justify-center"
        >
        <div
          class="lg:flex content-center place-content-center justify-center lg:p-0 max-w-1/4 lg:w-auto"
            @mouseover="hover = true"
            @mouseleave="hover = false"
        >
            <!-- <Menu as="div" class="relative inline-block text-right mx-1 lg:hidden">
              <div>
                <MenuButton
                  class="inline-flex justify-center w-full rounded-md border border-gray-300 shadow-sm px-4 py-2 bg-white text-sm font-medium text-gray-700 hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-100 focus:ring-green-800"
                >
                  Edit Text
                  <ChevronDownIcon class="-mr-1 ml-2 h-5 w-5" aria-hidden="true" />
                </MenuButton>
              </div>

              <transition
                enter-active-class="transition ease-out duration-100"
                enter-from-class="transform opacity-0 scale-95"
                enter-to-class="transform opacity-100 scale-100"
                leave-active-class="transition ease-in duration-75"
                leave-from-class="transform opacity-100 scale-100"
                leave-to-class="transform opacity-0 scale-95"
              >
                <MenuItems
                  class="origin-top-right absolute right-0 mt-2 w-full rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none"
                >
                  <div class="py-1">
                    <MenuItem v-slot="{ active }">
                    <a href="#" :class="[active ? 'bg-gray-100 text-gray-900' : 'text-gray-700', 'block px-4 py-2 text-sm']">Works?</a>
                    </MenuItem>

                    <MenuItem v-slot="{ active }">
                      <a
                        href="#"
                        @click="editor.chain().focus().toggleBold().run()"
                        :class="[{ 'is-active': editor.isActive('bold') }, 'block px-4 py-2 text-sm']"
                      >Bold</a>
                    </MenuItem>

                    <MenuItem v-slot="{ active }">
                      <a
                        href="#"
                        @click="editor.chain().focus().toggleItalic().run()"
                        :class="[{ 'is-active': editor.isActive('italic') }, 'block px-4 py-2 text-sm']"
                      >Italic</a>
                    </MenuItem>

                    <MenuItem v-slot="{ active }">
                      <a
                        href="#"
                        @click="editor.chain().focus().toggleItalic().run()"
                        :class="[{ 'is-active': editor.isActive('italic') }, 'block px-4 py-2 text-sm']"
                      >Italic</a>
                    </MenuItem>

                  </div>
                </MenuItems>
              </transition>
            </Menu>-->

            <!-- <div class='lg:hidden'>
              <button
                class="btn btn-large"
                title="Add Table"
                @click="editor.chain().focus().insertTable({ rows: 3, cols: 3, withHeaderRow: true }).run()"
              >
                <img class="w-4 lg:w-6" src="../../images/insert_table.png" alt="insert table icon" />
              </button>
            </div>-->

            <div v-if="!hideTextEdit" class="lg:block">
              <button
                class="btn btn-large font-bold"
                title="Bold"
                @click="editor.chain().focus().toggleBold().run()"
                :class="{ 'is-active': editor.isActive('bold') }"
              >
                <img class="w-4 lg:w-6" src="../../images/bold.png" alt="bold icon" title="Bold" />
              </button>

              <button
                class="btn btn-large italic"
                title="Italic"
                @click="editor.chain().focus().toggleItalic().run()"
                :class="{ 'is-active': editor.isActive('italic') }"
              >
                <img class="w-4 lg:w-6" src="../../images/italic-font.png" alt="italic icon" />
              </button>

              <button
                class="btn btn-large line-through"
                title="Strikethrough"
                @click="editor.chain().focus().toggleStrike().run()"
                :class="{ 'is-active': editor.isActive('strike') }"
              >
                <img
                  class="w-4 lg:w-6"
                  src="../../images/strikethrough.png"
                  alt="strikethrough icon"
                />
              </button>

              <button class="btn btn-large" @click="editor.chain().focus().unsetAllMarks().run()">
                <img
                  class="w-4 lg:w-6"
                  src="../../images/clear-format.png"
                  alt="clear formatting icon"
                  title="Clear Formatting"
                />
              </button>

              <button
                class="btn btn-large"
                title="Code Block"
                @click="editor.chain().focus().toggleCodeBlock().run()"
                :class="{ 'is-active': editor.isActive('codeBlock') }"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-6 w-4 lg:w-6"
                  fill="none"
                  viewBox="0 0 24 24"
                  stroke="currentColor"
                >
                  <path
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4"
                  />
                </svg>
              </button>

              <button
                class="btn btn-large"
                @click="editor.chain().focus().toggleBlockquote().run()"
                :class="{ 'is-active': editor.isActive('blockquote') }"
              >
                <img
                  class="w-4 lg:w-6"
                  src="../../images/quote.png"
                  alt="blockquote icon"
                  title="Blockquote"
                />
              </button>



              <button
                class="btn btn-large"
                title="Add Horizontal Line"
                @click="editor.chain().focus().setHorizontalRule().run()"
              >
                <img class="w-4 lg:w-6" src="../../images/line.png" alt="add line icon" />
              </button>

              <button
                class="btn btn-large"
                title="Add Line Break"
                @click="editor.chain().focus().setHardBreak().run()"
              >
                <img class="w-4 lg:w-6" src="../../images/break.png" alt="line break icon" />
              </button>
          </div>
          </div>

          <!-- <div class="invisible lg:visible lg:flex lg:content-center">
            <img class="w-4 lg:w-6" src="../../images/vertical-line.png" alt="divider line icon" />
          </div> -->

          <div v-if="!hideTableEdit" class="lg:p-0 lg:flex content-center max-w-1/4 lg:w-auto justify-center">
            <button
              class="btn btn-large"
              title="Add Table"
              @click="editor.chain().focus().insertTable({ rows: 3, cols: 3, withHeaderRow: true }).run()"
            >
              <img class="w-4 lg:w-6" src="../../images/insert_table.png" alt="insert table icon" />
            </button>

            <button
              class="btn btn-large"
              title="Add Column Left"
              @click="editor.chain().focus().addColumnBefore().run()"
              :disabled="!editor.can().addColumnBefore()"
            >
              <img
                class="w-4 lg:w-6"
                src="../../images/add_column_left.png"
                alt="add column before icon"
              />
            </button>

            <button
              class="btn btn-large"
              title="Add Column Right"
              @click="editor.chain().focus().addColumnAfter().run()"
              :disabled="!editor.can().addColumnAfter()"
            >
              <img
                class="w-4 lg:w-6"
                src="../../images/add_column_right.png"
                alt="add column after icon"
              />
            </button>

            <button
              class="btn btn-large"
              title="Delete Column"
              @click="editor.chain().focus().deleteColumn().run()"
              :disabled="!editor.can().deleteColumn()"
            >
              <img class="w-4 lg:w-6" src="../../images/delete_column.svg" alt="delete column icon" />
            </button>

            <button
              class="btn btn-large"
              title="Add Row Above"
              @click="editor.chain().focus().addRowBefore().run()"
              :disabled="!editor.can().addRowBefore()"
            >
              <img class="w-4 lg:w-6" src="../../images/add_row_above.png" alt="add row above icon" />
            </button>

            <button
              class="btn btn-large"
              title="Add Row Below"
              @click="editor.chain().focus().addRowAfter().run()"
              :disabled="!editor.can().addRowAfter()"
            >
              <img class="w-4 lg:w-6" src="../../images/add_row_below.png" alt="add row below icon" />
            </button>

            <button
              class="btn btn-large"
              title="Delete Row"
              @click="editor.chain().focus().deleteRow().run()"
              :disabled="!editor.can().deleteRow()"
            >
              <img class="w-4 lg:w-6" src="../../images/delete_row.svg" alt="delete row icon" />
            </button>

            <button
              class="btn btn-large table-delete"
              title="Delete Table"
              @click="editor.chain().focus().deleteTable().run()"
              :disabled="!editor.can().deleteTable()"
            >
              <img class="w-4 lg:w-6" src="../../images/delete_table.png" alt="delete table icon" />
            </button>

            <button
              class="btn btn-large"
              title="Merge Cells"
              @click="editor.chain().focus().mergeCells().run()"
              :disabled="!editor.can().mergeCells()"
            >
              <img class="w-4 lg:w-6" src="../../images/merge.png" alt="merge cells icon" />
            </button>

            <button
              class="btn btn-large"
              title="Split Cell"
              @click="editor.chain().focus().splitCell().run()"
              :disabled="!editor.can().splitCell()"
            >
              <img class="w-4 lg:w-6" src="../../images/split_cell.png" alt="split cell icon" />
            </button>

            <button
              class="btn btn-large previous"
              title="Next Cell"
              @click="editor.chain().focus().goToNextCell().run()"
              :disabled="!editor.can().goToNextCell()"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-6 w-4 lg:w-6"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M14 5l7 7m0 0l-7 7m7-7H3"
                />
              </svg>
            </button>

            <button
              class="btn btn-large next"
              title="Previous Cell"
              @click="editor.chain().focus().goToPreviousCell().run()"
              :disabled="!editor.can().goToPreviousCell()"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-6 w-4 lg:w-6"
                fill="none"
                viewBox="0 0 24 24"
                stroke="currentColor"
              >
                <path
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  stroke-width="2"
                  d="M10 19l-7-7m0 0l7-7m-7 7h18"
                />
              </svg>
            </button>
          </div>

          <!-- <div class="invisible lg:visible lg:flex lg:content-center">
            <img class="w-4 lg:w-6" src="../../images/vertical-line.png" alt="divider line icon" />
          </div> -->

          <div v-if="!hideTextEdit || !hideTableEdit" class="max-w-1/4 lg:w-auto lg:flex content-center lg:p-0">
            <button class="btn btn-large" title="Undo" @click="editor.chain().focus().undo().run()">
              <img class="w-4 lg:w-6" src="../../images/undo_round.png" alt="undo arrow icon" />
            </button>

            <button class="btn btn-large" title="Redo" @click="editor.chain().focus().redo().run()">
              <img class="w-4 lg:w-6" src="../../images/redo.png" alt="redo arrow icon" />
            </button>
          </div>
        </div>
      </div>
    </div>

  </div>

</template>

<script setup lang="ts" >

import { ref, reactive, onUnmounted, onMounted } from 'vue'
import { Editor, EditorContent, BubbleMenu } from '@tiptap/vue-3'
import { Menu, MenuButton, MenuItem, MenuItems } from '@headlessui/vue'
import { ChevronDownIcon } from '@heroicons/vue/solid'
import StarterKit from '@tiptap/starter-kit'
import Table from '@tiptap/extension-table'
import TableRow from '@tiptap/extension-table-row'
import TableCell from '@tiptap/extension-table-cell'
import TableHeader from '@tiptap/extension-table-header'
import { findDir } from '@vue/compiler-core'

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

const hover = ref(false)

const editor = new Editor({
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
  content: '',
})


onUnmounted(() => editor.destroy())

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
    background: #0d0d0d;
    color: #fff;
    font-family: "JetBrainsMono", monospace;
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
    border-left: 2px solid rgba(#0d0d0d, 0.1);
  }

  hr {
    border: none;
    border-top: 2px solid rgba(#0d0d0d, 0.1);
    margin: 2rem 0;
  }

  // min-height: 100%;
  // max-height: 80%;
  height: 100%;
  overflow-y: scroll;
  padding: 1%;

  // button {
  //   background-color: purple;
  // }
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
      background-color: whitesmoke;

      > * {
        margin-bottom: 0;
      }
    }

    th {
      font-weight: bold;
      text-align: left;
      background-color: #9CA884
      // background-color: rgb(209, 250, 213);
    }

    .selectedCell:after {
      z-index: 2;
      position: absolute;
      content: "";
      left: 0;
      right: 0;
      top: 0;
      bottom: 0;
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
