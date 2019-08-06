<template>
	<div id="app">
		<div class="projects">
			<div
				v-for="(project, index) in projects"
				:key="index"
				class="project hidden"
				:id="'project-' + index "
				@click="clickProject($event, index)"
				@mousemove="mousePosition($event, index)"
				@mouseenter="mouseEntered($event)"
				@mouseleave="mouseLeft($event)"
			>
				<div class="inner">
					<div class="shroud" :style="`left: ${project.spotlight.x}px; top: ${project.spotlight.y}px;`"></div>
					<img class="image" :src="imgUrl(project.image)" :alt="project.description" />
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
		clickProject(event, index) {
			let newId = event.currentTarget.id;
			let lastId = this.lastActiveId;
			let newActive = document.getElementById(newId);
			let lastActive = document.getElementById(lastId);

			if (newId != lastId) {
				lastActive.classList.remove("active");
			}
			newActive.classList.add("active");

			this.lastActiveId = newId;

			this.mousePosition(event, index);
		},
		mouseEntered(event) {
			document
				.getElementById(event.currentTarget.id)
				.classList.remove("hidden");
		},
		mouseLeft(event) {
			document
				.getElementById(event.currentTarget.id)
				.classList.add("hidden");
		},
		mousePosition(event, index) {
			let element = document
				.getElementById(event.currentTarget.id)
				.getBoundingClientRect();

			this.projects[index].spotlight.x = parseFloat(
				event.pageX - (element.left + window.scrollX + 40)
			);
			this.projects[index].spotlight.y = parseFloat(
				event.pageY - (element.top + window.scrollY + 40)
			);
		}
	},
	data() {
		return {
			lastActiveId: "project-0",
			projects: [
				{
					description:
						"I'm a <span>frontend developer</span> and <span>designer</span>. You can find my recent work on this page, or <a href='Dominic-Butler-CV.pdf' target='blank'>click here</a> to open my CV.",
					image: "avatar.jpg",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"A website for a small digital agency, built with <span>Vue</span>, <span>Nuxt</span> and <span>UI Kit</span>.",
					image: "discoverit.jpg",
					link: "https://discoverit.digital",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"Guitar theory made bright and lively with <span>Illustrator</span> and <span>After Effects</span>",
					image: "notecircle.jpg",
					link:
						"https://www.youtube.com/watch?v=JChDbIOkE58&list=PLrRbyFPS5q6w8wLmKAudLnPg1L7CMv1Lw",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"A collection of my <span>graphic design</span> and illustration work.",
					image: "teddy.jpg",
					link: "https://www.instagram.com/dombutlerpad/",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"An <span>interactive visualisation</span> showing the scale of planets in our solarsystem. Built with <span>D3</span>",
					image: "planets.jpg",
					link: "https://planet-scale.herokuapp.com",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"A model driven colour palette built with <span>React</span>.",
					image: "colourPalette.png",
					link: "https://material-colour-palette.herokuapp.com",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"Visualising progress through the year down to the second. Built with <span>D3</span>",
					image: "barclock.jpg",
					link: "https://bar-clock.herokuapp.com",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"A simple <span>React</span> app for recording statistical data during a race.",
					image: "runners.png",
					link: "https://dcsl-runners.herokuapp.com",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"A <span>Javascript</span> clock that changes colour.",
					image: "colourclock.jpg",
					link: "https://colour-clock.herokuapp.com",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"Experimenting with animation in <span>Javascript</span>",
					image: "helloworld.jpg",
					link: "https://hello-world-animation.herokuapp.com",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"MonoNote is minimalist note-pad app built with <span>React</span> and <span>Bootstrap</span>",
					image: "mononote.jpg",
					link: "https://mononote.herokuapp.com/",
					spotlight: { x: 0, y: 0 }
				},
				{
					description:
						"A simple <span>Javascript</span> memory game using the checkbox element.",
					image: "checkboxes.png",
					link: "https://checkbox-challenge.herokuapp.com",
					spotlight: { x: 0, y: 0 }
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
	font-family: fira-regular;
	src: url(assets/fonts/FiraCode-Regular.otf);
	font-display: block;
}
@font-face {
	font-family: fira-medium;
	src: url(assets/fonts/FiraCode-Medium.otf);
	font-display: block;
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
	&.hidden .shroud {
		opacity: 0;
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
	background: rgba(255, 255, 255, 0.4);
	@media (max-width: @small-screen) {
		width: 95vw;
		height: 95vw;
		opacity: 1;
	}
}

.inner .shroud {
	position: absolute;
	top: 0;
	left: 0;
	width: 1160px;
	height: 1160px;
	transition: opacity 0.4s;
	background: radial-gradient(at center, transparent, black);
	transform: translate(-580px, -580px);
	@media (max-width: @small-screen) {
		display: none;
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
	background-color: rgba(0, 0, 0, 0.1);
	display: flex;
	justify-content: center;
	align-items: center;
	padding: 30px;
	box-sizing: border-box;
	text-align: center;
	font-size: 20px;
	font-family: "fira-regular", monospace;
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
		font-family: "fira-medium", monospace;
		&:hover {
			text-decoration: underline;
		}
	}
	span {
		font-family: "fira-medium", monospace;
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
		background-color: darkslategray;
		.image {
			filter: blur(10px);
			opacity: 0.5;
			transform: scale(1.5);
		}
		.details {
			opacity: 1;
			pointer-events: all;
		}
	}
}
</style>

