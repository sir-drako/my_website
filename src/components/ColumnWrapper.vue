<template>
  <v-container class="mt-3">
    <v-row justify="center" no-gutters>
      <v-col cols="12" md="11" xl="10">
        <v-sheet elevation="5" :class="sheet_class">
          <!-- Content that this column wrapper wraps -->
          <slot></slot>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  props: {
    sheet_class: {
      type: String,
      default: '',
    }
  }
};
</script>
