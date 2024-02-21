<template>
  <Modal :show="true" @close="$emit('close')">
    <form autocomplete="off"
      class="bg-white dark:text-gray-400 bg-gray-100 dark:bg-gray-900 rounded-lg shadow-lg overflow-hidden"
      @submit.prevent="handleSubmit">
      <div>
        <heading :level="2" class="border-b border-40 py-4 px-2">{{ __('Create') }} "{{ group }}"</heading>

        <div class="p-3">
          <label class="inline-block text-80 mb-2 leading-tight nova-form-label">{{ __('Key of new translation')
          }}</label><br>
          <input type="text" ref="keyNameInput" required class="w-full form-control form-input form-input-bordered"
            v-model="keyName">
        </div>
      </div>
      <div class="bg-30 px-6 py-3 flex">
        <div class="flex items-center ml-auto">
          <CancelButton tabindex="0" dusk="cancel-create-button" type="button" @click="$emit('create-cancelled')" />

          <LoadingButton :loading="false" type="submit"
            class="shrink-0 h-9 px-4 focus:outline-none ring-primary-200 dark:ring-gray-600 focus:ring text-white dark:text-gray-800 inline-flex items-center font-bold shadow rounded focus:outline-none ring-primary-200 dark:ring-gray-600 focus:ring bg-primary-500 hover:bg-primary-400 active:bg-primary-600 text-white dark:text-gray-800 inline-flex items-center font-bold px-4 h-9 text-sm shrink-0 h-9 px-4 focus:outline-none ring-primary-200 dark:ring-gray-600 focus:ring text-white dark:text-gray-800 inline-flex items-center font-bold">
            <span>{{ __('Create') }}</span>
          </LoadingButton>
        </div>
      </div>
    </form>
  </Modal>
</template>

<script>
export default {
  name: "AddRowModal",
  props: {
    group: {},
    existingKeys: {}
  },
  data() {
    return {
      keyName: ''
    }
  },
  methods: {
    handleSubmit() {
      this.keyName = this.keyName.trim();
      if (this.existingKeys.indexOf(this.keyName) != -1) {
        Nova.error('This key is already in use');
      }
      else {
        this.$emit('create', this.keyName)
      }
    },
  },
  /**
   * Mount the component.
   */
  mounted() {
    //this.$refs.keyNameInput.focus()
  },
}
</script>

<style scoped></style>
