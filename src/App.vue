<template>
	<div id="app">
		<div class="projects">
			<div v-for="(project, index) in projects" :key="index">
				<div class="project-container" :id="'project-' + index " @click="clickProject($event)">
					<img class="image-glow" :src="imgUrl(project.image)">
					<div class="project">
						<img class="image" :src="imgUrl(project.image)" :alt="project.description">
						<div class="reverse">
							<p v-html="project.description"></p>
							<a class="visit-link" v-if="project.link" :href="project.link" target="blank">
								VISIT
								<div>-></div>
							</a>
						</div>
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
			document.getElementById("project-0").classList.add("project-active");
		},
		methods: {
			imgUrl: function(path) {
				return require(`./assets/${path}`);
			},
			clickProject(event) {
				let thisProject = document.getElementById(event.currentTarget.id);
				let lastProject = document.getElementById(this.lastProject);

				if (this.lastProject != event.currentTarget.id) {
					lastProject.classList.remove("project-active");
				}
				thisProject.classList.add("project-active");

				this.lastProject = event.currentTarget.id;
			}
		},
		data() {
			return {
				lastProject: "project-0",
				projects: [
					{
						description:
							"I'm a <span>frontend developer</span> and <span>designer</span>. You can find my recent work on this page, or <a href='Dominic Butler CV.pdf' target='blank'>click here</a> to open my CV.",
						image: "avatar.png"
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
						image: "notecircle.png",
						link:
							"https://www.youtube.com/watch?v=JChDbIOkE58&list=PLrRbyFPS5q6w8wLmKAudLnPg1L7CMv1Lw"
					},
					{
						description:
							"A collection of my <span>graphic design</span> and illustration work.",
						image: "teddy.png",
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
						image: "cafes.png",
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
						image: "mononote.png",
						link: "https://mononote.herokuapp.com/"
					},
					{
						description:
							"A simple <span>Javascript</span> memory game using the checkbox element.",
						image: "checkboxes.png",
						link: "https://checkbox-challenge.herokuapp.com"
					},
					{
						description:
							"An album cover layout. Experimenting with <span>CSS</span> styles.",
						image: "albumtable.png",
						link: "https://album-wall.herokuapp.com"
					}
				]
			};
		}
	};
</script>

<style lang="less">
	html {
		background-color: black;
	}
	body {
		margin: 0;
	}

	@font-face {
		font-family: fira-code;
		src: url(assets/fonts/FiraCode-Regular.otf);
	}

	.projects {
		display: flex;
		justify-content: center;
		flex-wrap: wrap;
		margin: 100px 0;
	}

	.project-container {
		padding: 40px;
		position: relative;
		@media (max-width: 600px) {
			padding: 30px 10px;
		}
	}

	.image-glow {
		object-fit: cover;
		width: 100%;
		height: 100%;
		position: absolute;
		top: 0;
		left: 0;
		filter: blur(100px) saturate(200%);
		-webkit-filter: blur(100px) saturate(200%);
		opacity: 0;
		transition: 0.2s;
	}

	.project {
		position: relative;
		width: 500px;
		height: 500px;
		// margin: 40px;
		overflow: hidden;
		cursor: pointer;
		border-radius: 5px;
		transition: 0.2s;
		opacity: 0.3;
		& > * {
			position: absolute;
			top: 0;
			left: 0;
			transition: 0.2s;
		}
		@media (max-width: 600px) {
			width: 90vw;
			height: 90vw;
		}

		img {
			object-fit: cover;
			width: 100%;
			height: 100%;
		}

		.reverse {
			color: white;
			opacity: 0;
			width: 100%;
			height: 100%;
			background-color: rgba(0, 0, 0, 0.3);
			display: flex;
			justify-content: center;
			align-items: center;
			flex-direction: column;
			padding: 50px;
			box-sizing: border-box;
			text-align: center;
			font-size: 20px;
			font-family: "fira-code";
			line-height: 1.5;
			pointer-events: none;
			@media (max-width: 600px) {
				font-size: 15px;
			}

			p {
				a {
					color: #fff54e;
					text-decoration: none;
				}
				span {
					color: rgb(116, 255, 128);
				}
			}

			.visit-link {
				text-decoration: none;
				color: #fff54e;
				padding: 10px;
				display: flex;
				cursor: pointer;
				position: absolute;
				bottom: 10px;
				right: 15px;
				div {
					transition: 0.2s;
					padding-left: 5px;
				}
			}
		}
		@media (max-width: 600px) {
			opacity: 1;
		}
	}

	.project-container:hover {
		z-index: 1000;
		.project {
			opacity: 1;
			transform: scale(1.03);
		}
		.image-glow {
			opacity: 0.3;
		}
	}

	.project-container.project-active,
	.project-container.project-active:hover {
		z-index: 2000;

		.project {
			opacity: 1;
			transform: scale(1.03);
			cursor: default;
			img {
				filter: brightness(200%) blur(70px) saturate(200%);
				-webkit-filter: brightness(200%) blur(70px) saturate(200%);
				opacity: 1;
				transform: scale(1.2);
			}

			.reverse {
				opacity: 1;
				pointer-events: all;
			}
		}
		.image-glow {
			opacity: 0.3;
		}
	}
</style>

