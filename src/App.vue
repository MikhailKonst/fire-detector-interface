<template>
	<div class="app">
		<CheckHealth :messageTypes="messageTypes" />
		<FireDetection :messageTypes="messageTypes" />
	</div>
</template>

<script setup lang="ts">
import CheckHealth from '@/components/CheckHealth/CheckHealth.vue';
import FireDetection from '@/components/FireDetection/FireDetection.vue';
import { ref, onMounted } from 'vue';
import { fetchData } from './components/mocks/db';

const messageTypes = ref<{ class: string; message: string }[]>([]);

const loadMessageTypes = async () => {
	try {
		messageTypes.value = await fetchData('/message-types');
	} catch (error) {
		console.error('Ошибка загрузки:', error);
	}
};

onMounted(loadMessageTypes);
</script>

<style lang="scss" scoped>
@import './styles/main.scss';

.app {
	padding: 20px;
	margin: 0 auto;
	max-width: fit-content;
	width: 100%;
	border: $border-width solid $color-border;
	border-radius: $border-radius;
	box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	background-color: $color-bg;
	font-family: $font-stack;
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;

	@media (max-width: 768px) {
		padding: 15px;
		max-width: 90%;
	}

	@media (max-width: 480px) {
		padding: 10px;
		max-width: 100%;
	}
}
</style>
