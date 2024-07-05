<script>
	import { onMount } from 'svelte';

	let sidebar;

	onMount(() => {
		const handleMouseMove = (event) => {
			const { clientX, clientY } = event;
			const { left, top, width, height } = sidebar.getBoundingClientRect();
			const x = clientX - left - width / 2;
			const y = clientY - top - height / 2;

			const rotateX = (y / height) * -15; // Adjust the sensitivity here
			const rotateY = (x / width) * 15; // Adjust the sensitivity here

			sidebar.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
		};

		const handleMouseLeave = () => {
			sidebar.style.transform = 'perspective(1000px) rotateX(0) rotateY(0)';
		};

		sidebar.addEventListener('mousemove', handleMouseMove);
		sidebar.addEventListener('mouseleave', handleMouseLeave);

		return () => {
			sidebar.removeEventListener('mousemove', handleMouseMove);
			sidebar.removeEventListener('mouseleave', handleMouseLeave);
		};
	});
</script>

<aside bind:this={sidebar} class="sidebar">
	<div class="title">
		<h1>David<br />Hunt</h1>
	</div>
	<nav>
		<ul>
			<li><a href="#about">About</a></li>
			<li><a href="#experience">Experience</a></li>
			<li><a href="#projects">Projects</a></li>
		</ul>
	</nav>
</aside>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Abril+Fatface&display=swap');

	/* Sidebar Style */
	.sidebar {
		position: relative;
		margin-right: 20px;
		background: linear-gradient(135deg, #0292be, #66248d); /* Gradient background for style */
		border-radius: 40px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
		padding: 20px;
		text-align: center; /* Center the text */
		max-height: 450px;
		transition: transform 0.5s; /* Smooth transition for hover effect */
		transform-style: preserve-3d; /* Enable 3D transformations */
		overflow: hidden;
	}

	.sidebar h1 {
		margin-top: 20px;
		font-size: 3.5rem; /* Increase font size for emphasis */
		font-family: 'Abril Fatface', serif;
		font-weight: 700;
		font-optical-sizing: auto;
		color: rgba(255, 255, 255, 0); /* Make text invisible */
		-webkit-text-stroke: 2px white; /* Apply a white stroke to the text */
		position: relative;
		z-index: 1;
	}

	.sidebar h1::before {
		content: '';
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: inherit; /* Inherit the gradient background */
		z-index: -1;
		/* -webkit-mask: url(#mask) repeat-x; */
		/* mask: url(#mask) repeat-x; */
	}

	.sidebar p {
		font-family: 'Josefin Sans', sans-serif;
		color: #34495e; /* Slightly lighter color for the subtitle */
		font-size: 1rem;
		margin-bottom: 20px;
	}

	.sidebar nav ul {
		list-style-type: none; /* Remove default bullets */
		padding: 0;
		margin: 0;
	}

	.sidebar nav ul li {
		margin: 10px 0;
	}

	.sidebar nav ul li a {
		text-decoration: none;
		color: #e4e4e4;
		font-weight: bold;
		padding: 10px 15px; /* Add padding for better click area */
		display: block; /* Make the link a block element */
		border-radius: 15px; /* Rounded corners for links */
		transition:
			background-color 0.3s ease,
			color 0.3s ease; /* Smooth hover transition */
	}

	.sidebar nav ul li a:hover {
		background-color: #d5dee5; /* Change background color on hover */
		color: #161616; /* Change text color on hover */
	}
</style>
