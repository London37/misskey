<template>
<!-- eslint-disable vue/no-mutating-props -->
<XContainer :draggable="true" @remove="() => emit('remove')">
	<!-- Use a code icon (ti-code) and your new label -->
	<template #header><i class="ti ti-code"></i> {{ i18n.ts._pages.blocks.html }}</template>

	<section>
		<!-- We use blockContent instead of text -->
		<textarea v-model="blockContent" :class="$style.textarea" placeholder="<div>Hello World</div>"></textarea>
	</section>
</XContainer>
</template>

<script lang="ts" setup>
import { watch, ref } from 'vue';
import * as Misskey from 'misskey-js';
import XContainer from '../page-editor.container.vue';
import { i18n } from '@/i18n.js';

const props = defineProps<{
	modelValue: Misskey.entities.PageBlock & { type: 'html' }
}>();

const emit = defineEmits<{
	(ev: 'update:modelValue', value: Misskey.entities.PageBlock & { type: 'html' }): void;
	(ev: 'remove'): void;
}>();

// Initialize the local ref with 'content' instead of 'text'
const blockContent = ref(props.modelValue.content ?? '');

// Watch for changes and emit the update to the parent editor
watch(blockContent, () => {
	emit('update:modelValue', {
		...props.modelValue,
		content: blockContent.value,
	});
});
</script>

<style lang="scss" module>
.textarea {
	display: block;
	width: 100%;
	min-width: 100%;
	max-width: 100%;
	min-height: 150px;
	resize: vertical;
	margin: 0;
	padding: 8px;
	font-family: monospace; /* Better for editing HTML code */
	border: none;
	border-radius: 0;
	background: transparent;
	color: var(--fg);
}
</style>
