<script setup lang="ts">
import { ref } from "vue";
import type { ImageWithStory } from "./types";

const imageWithStoryList: ImageWithStory[] = [
	{ src: "satya-cool-car.jpeg", title: "Cool Drive", body: "Looking pretty suave yeah." },
	{ src: "satya-cafe-1.jpeg", title: "Nonchalant Time in Cafe", body: "Lorem ipsum dolor sit amet consectetur adipisicing elit. Magni, fuga! Corporis, laudantium suscipit laborum voluptatum obcaecati animi rerum consectetur tempore voluptates dolorum culpa nihil placeat officia soluta illum. Molestiae, facere." },
	{ src: "satya-rad.jpeg", title: "Rad Joke", body: "When you can pose quite a bit nonchalant because you love your daughter" },
	{ src: "satya-stuti-sofa-gnome.jpeg", title: "Sofa Gnome", body: "For the lazy days innit" },
];

const currentlySelectedImage = ref<ImageWithStory | null>(imageWithStoryList[0]);

// Only select an image if no image is currently selected
const selectImage = (image: ImageWithStory) => !currentlySelectedImage.value && (currentlySelectedImage.value = image);

const clearSelectedImage = () => currentlySelectedImage.value = null;
</script>

<template>
	<header class="center">
		<h1 class="mb-n-1">The Best Son, Husband, Father, and Friend</h1>
		<h2>Satya Prakash Pachisia</h2>
		<img class="br-20" src="/satya-rad.jpeg" alt="Rad Dad" width="300">
		<p class="mw-450px text-g-400 text-left">
			Lorem ipsum dolor sit amet consectetur adipisicing elit. Magni, fuga! Corporis, laudantium suscipit laborum
			voluptatum obcaecati animi rerum consectetur tempore voluptates dolorum culpa nihil placeat officia soluta
			illum. Molestiae, facere.
		</p>
	</header>
	<main class="mt-1 grid-repeat max-w-650px">
		<div v-for="item in imageWithStoryList" :key="item.src">
			<img class="br-20 hov-scale" :src="item.src" style="height: 350px; object-fit: cover;" :alt="item.title"
				@click="() => selectImage(item)" />
		</div>
		<div v-if="currentlySelectedImage" class="card-display">
			<button @click="() => clearSelectedImage()" class="dismiss-button"
				style="position: absolute; top: 5px; right: 5px;">✖</button>
			<div class="card-body">
				<img :src="currentlySelectedImage.src" :alt="currentlySelectedImage.title" class="card-image" />
				<div class="card-text">
					<h2>{{ currentlySelectedImage.title }}</h2>
					<p>{{ currentlySelectedImage.body }}</p>
				</div>
			</div>
		</div>
	</main>
</template>

<style scoped>
.center {
	display: grid;
	justify-items: center;
	text-align: center;
}

.grid-repeat {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
	justify-content: center;
	justify-items: center;
	gap: 1em 0;
	padding: 0 0.5em;
}

.br-20 {
	border-radius: 20px;
}

.br-6 {
	border-radius: 6px;
}

.mb-1 {
	margin-bottom: 1em;
}

.mt-1 {
	margin-top: 3em;
}

.mw-450px {
	max-width: 450px;
}

.mw-650px {
	max-width: 650px;
}

.text-g-400 {
	color: gray;
}

.mb-n-1 {
	margin-bottom: -0.5em;
}

.text-left {
	text-align: left;
}

.hov-scale:hover {
	transform: scale(1.03);
	transition-timing-function: ease-out;
	transition-duration: 400ms;
}

.card-display {
	box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.2);
	position: fixed;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	z-index: 2;
	background-color: white;
	border-radius: 20px;
}

.card-body {
	display: grid;
	border-radius: 20px;
	min-width: 33vw;
}

.card-text {
	padding: 3em;
}

.card-image {
	width: 100%;
	border-top-left-radius: 20px;
	border-top-right-radius: 20px;
	max-height: 400px;
	object-fit: cover;
}

.dismiss-button {
	float: right;
	background: none;
	border: none;
	font-size: 1.5em;
	margin-top: 1em;
	margin-right: 1em;
	color: gray;
}
</style>
