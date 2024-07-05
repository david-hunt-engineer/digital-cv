<script>
	import { onMount } from 'svelte';

	let shadow; // This will be bound to the shadow element
	let sidebar; // This will be bound to your panel element

	onMount(() => {
		const handleMouseMove = (event) => {
			const { clientX, clientY } = event;
			const { left, top, width, height } = sidebar.getBoundingClientRect();
			const x = clientX - left - width / 2;
			const y = clientY - top - height / 2;

			const rotateX = (y / height) * -15; // Adjust the sensitivity here
			const rotateY = (x / width) * 15; // Adjust the sensitivity here

			sidebar.style.transform = `perspective(1000px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;

			// Shadow calculations
			const shadowOffsetX = 20 + (x / width) * 20; // Adjust shadow X position based on light source
			const shadowOffsetY = 20 + (y / height) * 20; // Adjust shadow Y position based on light source
			shadow.style.transform = `translateX(${shadowOffsetX}px) translateY(${shadowOffsetY}px)`;
		};

		const handleMouseLeave = () => {
			sidebar.style.transform = 'perspective(1000px) rotateX(0) rotateY(0)';
			shadow.style.transform = 'translateX(20px) translateY(20px)';
		};

		sidebar.addEventListener('mousemove', handleMouseMove);
		sidebar.addEventListener('mouseleave', handleMouseLeave);

		return () => {
			sidebar.removeEventListener('mousemove', handleMouseMove);
			sidebar.removeEventListener('mouseleave', handleMouseLeave);
		};
	});
</script>

<div bind:this={shadow} class="shadow"></div>
<!-- Shadow element should be before the sidebar -->
<div bind:this={sidebar} class="sidebar">
	<svg width="300" height="200" xmlns="http://www.w3.org/2000/svg">
		<defs>
			<mask id="cutout-text">
				<rect width="100%" height="100%" fill="white" />
				<text x="50%" y="50%" dominant-baseline="middle" text-anchor="middle" font-size="40" fill="black"
					>David<br />Hunt</text
				>
			</mask>
			<linearGradient id="gradient" x1="0%" y1="0%" x2="100%" y2="100%">
				<stop offset="0%" style="stop-color:#0292be; stop-opacity:1" />
				<stop offset="100%" style="stop-color:#66248d; stop-opacity:1" />
			</linearGradient>
		</defs>
		<rect width="100%" height="100%" fill="url(#gradient)" mask="url(#cutout-text)" rx="40" ry="40" />
	</svg>
	<nav>
		<ul>
			<li><a href="#about">About</a></li>
			<li><a href="#experience">Experience</a></li>
			<li><a href="#projects">Projects</a></li>
		</ul>
	</nav>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Stardos+Stencil:wght@400;700&display=swap');

	.sidebar,
	.shadow {
		width: 300px;
		height: 300px; /* Adjusted to fit the nav content */
		position: absolute;
		left: 100px;
		top: 100px;
	}

	.sidebar {
		display: flex;
		flex-direction: column; /* Arrange items vertically */
		align-items: center;
		justify-content: center;
		transition: transform 0.1s;
		transform-style: preserve-3d;
		z-index: 99;
		border-radius: 40px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
		background-color: rgb(255, 255, 255);

		/* overflow: hidden; */
	}

	.shadow {
		background-color: rgba(0, 0, 0, 0.3);
		transition: transform 0.1s;
		transform: translateX(20px) translateY(20px);
		z-index: -1; /* Ensure the shadow is behind the sidebar */
		filter: blur(5px);
		border-radius: 10px;
	}

	nav ul {
		list-style-type: none; /* Remove default bullets */
		padding: 0;
		margin: 20px 0 0 0; /* Adjust margin for spacing */
		text-align: center; /* Center the text */
	}

	nav ul li {
		margin: 10px 0;
	}

	nav ul li a {
		text-decoration: none;
		color: #e4e4e4;
		font-weight: bold;
		padding: 10px 15px; /* Add padding for better click area */
		display: block; /* Make the link a block element */
		border-radius: 15px; /* Rounded corners for links */
		transition:
			background-color 0.1s ease,
			color 0.1s ease; /* Smooth hover transition */
	}

	nav ul li a:hover {
		background-color: #d5dee5; /* Change background color on hover */
		color: #161616; /* Change text color on hover */
	}
</style>
