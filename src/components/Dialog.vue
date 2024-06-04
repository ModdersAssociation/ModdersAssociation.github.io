<script setup lang="ts">
import {
  TransitionRoot,
  TransitionChild,
  Dialog,
  DialogPanel,
  DialogTitle,
} from '@headlessui/vue'
import type { Ref } from 'vue'
import {ref,onMounted} from 'vue'
const isOpen = ref(false)
const modalData: Ref<{links: string[]; versions: string[]}> = ref([]);
function closeModal() {
  isOpen.value = false
}
function openModal() {
  isOpen.value = true
}

onMounted(() => {
  document.body.addEventListener("download", (e) => {
    modalData.value = e.detail;
    console.log(modalData.value);
    openModal()
  })
})

</script>


<template>
  <TransitionRoot appear :show="isOpen" as="template">
    <Dialog as="div" @close="closeModal" class="relative z-10">
      <TransitionChild
        as="template"
        enter="duration-300 ease-out"
        enter-from="opacity-0"
        enter-to="opacity-100"
        leave="duration-200 ease-in"
        leave-from="opacity-100"
        leave-to="opacity-0"
      >
        <div class="fixed inset-0 bg-black/90" />
      </TransitionChild>

      <div class="fixed inset-0 overflow-y-auto">
        <div
          class="flex min-h-full items-center justify-center p-4 text-center"
        >
          <TransitionChild
            as="template"
            enter="duration-300 ease-out"
            enter-from="opacity-0 scale-95"
            enter-to="opacity-100 scale-100"
            leave="duration-200 ease-in"
            leave-from="opacity-100 scale-100"
            leave-to="opacity-0 scale-95"
          >
            <DialogPanel
              class="w-full max-w-md transform overflow-hidden rounded-2xl bg-white p-6 text-left align-middle shadow-xl transition-all"
            >
              <DialogTitle
                as="h3"
                class="text-lg font-medium leading-6 text-gray-900"
              >
                Download
              </DialogTitle>
              <div class="mt-2 flex  flex-col items-center">
                <a v-for="download,i in modalData.links" :href="download" class="block w-fit px-10 mt-2 rounded-md bg-purple-600 text-white font-bold py-2 hover:bg-purple-500 transition-all active:scale-90 ease-out">{{ modalData.versions[i] }} </a>
              </div>

              <div class="mt-4">
                <button
                  type="button"
                  class="inline-flex justify-center rounded-md border border-transparent bg-blue-100 px-4 py-2 text-sm font-medium text-blue-900 hover:bg-blue-200 focus:outline-none focus-visible:ring-2 focus-visible:ring-blue-500 focus-visible:ring-offset-2"
                  @mouseup="closeModal"
                >
                  Ok.
                </button>
              </div>
            </DialogPanel>
          </TransitionChild>
        </div>

      </div>
    </Dialog>
  </TransitionRoot>
</template>import type ts from 'typescript';
