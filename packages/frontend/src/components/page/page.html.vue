<template>
  <!-- v-html renders the raw string from the database as HTML -->
  <div v-html="block.content" class="custom-html-block"></div>
</template>

<script lang="ts" setup>
import * as Misskey from 'misskey-js';

defineProps<{
	block: Misskey.entities.PageBlock,
	page: Misskey.entities.Page,
}>();
</script>
