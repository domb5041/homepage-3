<template>
	<div id="app">
		<div class="projects">
			<div
				v-for="(project, index) in projects"
				:key="index"
				class="project"
				:id="'project-' + index "
				@click="clickProject($event)"
				@mousemove="mousePosition($event)"
			>
				<div
					class="inner"
					:style="`background: radial-gradient(at ${panda.x}px ${panda.y}px, azure, darkslategrey)`"
				>
					<img class="image" :src="imgUrl(project.image)" :alt="project.description">
					<div class="details">
						<p class="text" v-html="project.description"></p>
						<a class="visit" v-if="project.link" :href="project.link" target="blank">VISIT-></a>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default {
		name: "app",
		components: {},
		mounted() {
			document.getElementById(this.lastActiveId).classList.add("active");
		},
		methods: {
			imgUrl: function(path) {
				return require(`./assets/${path}`);
			},
			clickProject(event) {
				let newId = event.currentTarget.id;
				let lastId = this.lastActiveId;
				let newActive = document.getElementById(newId);
				let lastActive = document.getElementById(lastId);

				if (newId != lastId) {
					lastActive.classList.remove("active");
				}
				newActive.classList.add("active");

				this.lastActiveId = newId;

				this.mousePosition(event);
			},
			mousePosition(event) {
				let element = document
					.getElementById(event.currentTarget.id)
					.getBoundingClientRect();

				if (event.currentTarget.id == this.lastActiveId) {
					this.panda.x = parseFloat(
						event.pageX - (element.left + window.scrollX + 40)
					);
					this.panda.y = parseFloat(
						event.pageY - (element.top + window.scrollY + 40)
					);
				}
			}
		},
		data() {
			return {
				lastActiveId: "project-0",
				panda: { x: 0, y: 0 },
				projects: [
					{
						description:
							"I'm a <span>frontend developer</span> and <span>designer</span>. You can find my recent work on this page, or <a href='Dominic Butler CV.pdf' target='blank'>click here</a> to open my CV.",
						image: "avatar.jpg"
					},
					{
						description:
							"A website for a small digital agency, built with <span>Vue</span>, <span>Nuxt</span> and <span>UI Kit</span>.",
						image: "discoverit.jpg",
						link: "https://discoverit.digital"
					},
					{
						description:
							"Guitar theory made bright and lively with <span>Illustrator</span> and <span>After Effects</span>",
						image: "notecircle.jpg",
						link:
							"https://www.youtube.com/watch?v=JChDbIOkE58&list=PLrRbyFPS5q6w8wLmKAudLnPg1L7CMv1Lw"
					},
					{
						description:
							"A collection of my <span>graphic design</span> and illustration work.",
						image: "teddy.jpg",
						link: "https://www.instagram.com/dombutlerpad/"
					},
					{
						description:
							"An <span>interactive visualisation</span> showing the scale of planets in our solarsystem. Built with <span>D3</span>",
						image: "planets.jpg",
						link: "https://planet-scale.herokuapp.com"
					},
					{
						description:
							"A model driven colour palette built with <span>React</span>.",
						image: "colourPalette.png",
						link: "https://material-colour-palette.herokuapp.com"
					},
					{
						description:
							"Visualising progress through the year down to the second. Built with <span>D3</span>",
						image: "barclock.jpg",
						link: "https://bar-clock.herokuapp.com"
					},
					{
						description:
							"Connecting to Kentico Cloud API. built with <span>React</span>.",
						image: "cafes.jpg",
						link: "https://kentico-cafes.herokuapp.com/"
					},
					{
						description:
							"A simple <span>React</span> app for recording statistical data during a race.",
						image: "runners.png",
						link: "https://dcsl-runners.herokuapp.com"
					},
					{
						description:
							"A <span>Javascript</span> clock that changes colour.",
						image: "colourclock.jpg",
						link: "https://colour-clock.herokuapp.com"
					},
					{
						description:
							"Experimenting with animation in <span>Javascript</span>",
						image: "helloworld.jpg",
						link: "https://hello-world-animation.herokuapp.com"
					},
					{
						description:
							"MonoNote is minimalist note-pad app built with <span>React</span> and <span>Bootstrap</span>",
						image: "mononote.jpg",
						link: "https://mononote.herokuapp.com/"
					},
					{
						description:
							"A simple <span>Javascript</span> memory game using the checkbox element.",
						image: "checkboxes.png",
						link: "https://checkbox-challenge.herokuapp.com"
					}
				]
			};
		}
	};
</script>

<style lang="less">
	@small-screen: 580px;

	html {
		background-color: black;
	}
	body {
		margin: 0;
		text-align: center;
	}

	@font-face {
		font-family: fira-code;
		src: url(assets/fonts/FiraCode-Regular.otf);
		font-display: fallback;
	}

	.projects {
		display: flex;
		justify-content: center;
		flex-wrap: wrap;
		margin: 100px auto;
		max-width: 1800px;
	}

	.project {
		padding: 40px;
		position: relative;
		cursor: pointer;
		@media (max-width: @small-screen) {
			padding: 40px 0;
		}
	}

	.project .inner {
		position: relative;
		width: 500px;
		height: 500px;
		overflow: hidden;
		border-radius: 5px;
		transition: 0.2s;
		opacity: 0.3;
		@media (max-width: @small-screen) {
			width: 95vw;
			height: 95vw;
			opacity: 1;
		}
	}

	.inner .image {
		object-fit: cover;
		width: 100%;
		height: 100%;
		transition: 0.2s;
	}

	.inner .details {
		position: absolute;
		top: 0;
		left: 0;
		transition: 0.2s;
		color: white;
		opacity: 0;
		width: 100%;
		height: 100%;
		background-color: rgba(0, 0, 0, 0.3);
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 30px;
		box-sizing: border-box;
		text-align: center;
		font-size: 20px;
		font-family: "fira-code", monospace;
		line-height: 1.5;
		pointer-events: none;
		@media (max-width: @small-screen) {
			font-size: 4.5vw;
			padding: 5vw;
		}
	}

	.details .text,
	.details {
		a {
			color: #fff54e;
			text-decoration: none;
			&:hover {
				text-decoration: underline;
			}
		}
		span {
			color: rgb(116, 255, 128);
		}
	}

	.details .visit {
		padding: 30px;
		position: absolute;
		bottom: 0;
		right: 0;
		@media (max-width: @small-screen) {
			padding: 5vw;
		}
	}

	.project:hover {
		.inner {
			opacity: 1;
			transform: scale(1.03);
		}
	}

	.project.active,
	.project.active:hover {
		.inner {
			opacity: 1;
			transform: scale(1.03);
			cursor: default;
			// background: radial-gradient(at 60% 40px, white, silver, transparent);
			.image {
				filter: blur(10px);
				opacity: 0.6;
				transform: scale(1.5);
			}
			.details {
				opacity: 1;
				pointer-events: all;
			}
		}
	}
</style>

