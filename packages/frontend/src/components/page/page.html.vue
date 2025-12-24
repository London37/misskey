<template>
  <!-- v-html renders the raw string from the database as HTML -->
	<div :class="$style.htmlRoot"> <!-- Might change to $style.mainAbout -->
  	<div v-html="block.content"></div>
	</div>
</template>

<script lang="ts" setup>
import * as Misskey from 'misskey-js';

const props = defineProps<{
	block: Extract<Misskey.entities.PageBlock, {type: 'html' }>,
	page: Misskey.entities.Page,
}>();
</script>

<!-- overflow-wrap prevents long HTML strings from breaking the layout -->
<style lang="scss" module>
.htmlRoot {
	width: 100%;
	overflow-wrap: break-word;
}
</style>
