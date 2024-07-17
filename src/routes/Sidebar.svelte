<script>
	import { onMount } from 'svelte';

	let isOpen = false;
	let windowWidth = window.innerWidth;
	let sidebar;
	let shadow;
	let startX;
	let startY;
	let endX;
	let endY;

	const touch = matchMedia('(hover: none)').matches;

	const updateWindowWidth = () => {
		windowWidth = window.innerWidth;
	};

	const handleMouseEnter = () => {
		if (windowWidth < 1000) {
			isOpen = true;
		}
	};

	const handleMouseMove = (event) => {
		const { clientX, clientY } = event;
		const { left, top, width, height } = sidebar.getBoundingClientRect();
		const x = clientX - left - width / 2;
		const y = clientY - top - height / 2;

		const rotateX = (y / height) * -15; // Adjust the sensitivity here
		const rotateY = (x / width) * 15; // Adjust the sensitivity here

		// Shadow calculations for sunlight
		let shadowOffsetX = 20 - (x / width) * 24; // Adjust shadow X position based on light source
		let shadowOffsetY = 20 + (y / height) * 24; // Adjust shadow Y position based on light source

		if (!touch) {
			sidebar.style.transform = `perspective(1400px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
			shadow.style.transform = `translateX(${shadowOffsetX}px) translateY(${shadowOffsetY}px) perspective(1300px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
			shadow.style.zIndex = `100`;
			sidebar.style.zIndex = `100`;
		} else {
			sidebar.style.transform = `perspective(1400px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;

			// Shadow calculations for sunlight coming from the right
			shadowOffsetX = 10 - (x / width) * 24; // Adjust shadow X position based on light source
			shadowOffsetY = 10 + (y / height) * 24; // Adjust shadow Y position based on light source

			// Apply the perspective transform to the shadow
			shadow.style.transform = `translateX(${shadowOffsetX}px) translateY(${shadowOffsetY}px) perspective(1300px) rotateX(${rotateX}deg) rotateY(${rotateY}deg)`;
			shadow.style.zIndex = `100`;
			sidebar.style.zIndex = `100`;
		}
	};

	const handleMouseLeave = () => {
		if (windowWidth < 1000) {
			isOpen = false;
			shadow.style.transform = 'translateX(-5px) translateY(30px)';
		}
	};

	const updateShadowSize = () => {
		const sidebarWidth = sidebar.getBoundingClientRect().width;
		shadow.style.width = `${sidebarWidth}px`;
		const sidebarHeight = sidebar.getBoundingClientRect().height;
		shadow.style.height = `${sidebarHeight}px`;
		shadow.style.zIndex = `100`;
		sidebar.style.zIndex = `100`;
	};

	function handleTouchStart(event) {
		const touch = event.touches[0];
		startX = touch.clientX;
		startY = touch.clientY;
	}

	function handleTouchMove(event) {
		const touch = event.touches[0];
		endX = touch.clientX;
		endY = touch.clientY;
	}

	function handleTouchEnd(event) {
		const diffX = endX - startX;
		const diffY = endY - startY;

		if (Math.abs(diffX) > Math.abs(diffY) && diffX > 50) {
			console.log('Swipe Right Detected');
			event.preventDefault();

			if (windowWidth < 1000) {
				isOpen = true;
			}
		} else if (Math.abs(diffX) > Math.abs(diffY) && diffX < -50) {
			console.log('Swipe Left Detected');

			if (windowWidth < 1000) {
				isOpen = false;
			}
		} else if (windowWidth < 1000 && isOpen == true) {
			if (windowWidth < 1000) {
				console.log('tap detected, close sidebar');
				isOpen = false;
			}
		}
	}

	onMount(() => {
		// Set the initial window width
		updateWindowWidth();

		// Add event listener to update width on resize
		window.addEventListener('resize', updateWindowWidth);

		// Initial width update
		updateShadowSize();

		// Add touch event listeners
		document.addEventListener('touchstart', handleTouchStart);
		document.addEventListener('touchmove', handleTouchMove);
		document.addEventListener('touchend', handleTouchEnd);

		// Add mouse event listeners
		sidebar.addEventListener('mouseenter', handleMouseEnter);
		sidebar.addEventListener('mousemove', handleMouseMove);
		sidebar.addEventListener('mouseleave', handleMouseLeave);

		// Resize observer to update shadow size on resize
		const resizeObserver = new ResizeObserver(() => updateShadowSize());
		resizeObserver.observe(sidebar);

		return () => {
			document.removeEventListener('touchstart', handleTouchStart);
			document.removeEventListener('touchmove', handleTouchMove);
			document.removeEventListener('touchend', handleTouchEnd);

			sidebar.removeEventListener('mouseenter', handleMouseEnter);
			sidebar.removeEventListener('mousemove', handleMouseMove);
			sidebar.removeEventListener('mouseleave', handleMouseLeave);
			resizeObserver.disconnect();
		};
	});
</script>

<aside class="sidebar-container">
	<div bind:this={shadow} class="shadow" class:open={isOpen}></div>
	<div bind:this={sidebar} class="sidebar" class:open={isOpen}>
		<div class="title">
			<h1>David<br />Hunt</h1>
		</div>
		<nav>
			<ul>
				<li><a href="#about">About</a></li>
				<li><a href="#experience">Experience</a></li>
				<li><a href="#education">Education</a></li>
				<li><a href="#projects">Projects</a></li>
			</ul>
			<svg
				class="pull-arrow-icon {isOpen ? 'rotate-180' : ''}"
				xmlns="http://www.w3.org/2000/svg"
				version="1.1"
				xmlns:xlink="http://www.w3.org/1999/xlink"
				xmlns:svgjs="http://svgjs.dev/svgjs"
				viewBox="300 61 100 100"
				><defs>
					<linearGradient id="SvgjsLinearGradient1000" gradientTransform="rotate(343, 0.5, 0.5)">
						<stop offset="0"></stop>
						<stop offset="1"></stop>
					</linearGradient>
				</defs><path
					class:open={isOpen}
					d="M307.025390625,71.7488784790039C311.3781559244792,73.75784698486328,388.6397399902344,105.63826395670573,388.6397399902344,109.41703796386719C388.6397399902344,113.19581197102865,311.3781559244792,140.83108561197918,307.025390625,142.60089111328125"
					stroke="url(#SvgjsLinearGradient1000)"
					fill="none"
					stroke-width="25"
					stroke-linecap="round"
				></path>
			</svg>
		</nav>
	</div>
</aside>

<style>
	@keyframes colorShift {
		0% {
			stop-color: hsl(205, 70%, 72%);
		}
		50% {
			stop-color: hsl(235, 83%, 66%);
		}
		100% {
			stop-color: hsl(205, 70%, 72%);
		}
	}

	#SvgjsLinearGradient1000 stop {
		animation: colorShift 5s Ease-in-out infinite;
	}
	.pull-arrow-icon {
		border-radius: 10px;
		padding: 5px;
		background-color: rgb(255, 255, 255, 0.5);
		width: 20px; /* Adjust based on your layout needs */
		position: absolute;
		top: 50%; /* Align vertically center */
		right: 0px; /* Align to the right edge of the sidebar */
		transform: translateY(-50%); /* Center vertically */
		display: block; /* Change to 'none' if you want it initially hidden */
		transition: transform 0.3s ease; /* Transition for all transform changes */
	}
	.rotate-180 {
		transform: translateY(-50%) rotate(180deg); /* Maintain vertical centering with rotation */
	}
	.sidebar-container {
		position: sticky;
		height: 100vh; /* Full viewport height */
		position: sticky; /* Make sidebar sticky */
		top: 0px; /* Stick to the top of the viewport */
		max-height: 100vh;
		justify-content: center;
		align-items: center;
		margin-left: 20px;
		margin-right: 20px;
		z-index: 0;
		max-width: 420px;
	}

	.sidebar {
		position: relative;
		min-width: 200px;
		margin-left: 10px;
		margin-right: 15px;
		border-radius: 40px;
		margin-bottom: 20px;

		padding: 50px;
		text-align: center;
		transform-style: flat;
		background-color: rgb(255, 255, 255);
		transition: transform 0.1s ease;
		z-index: 10;
	}

	.shadow {
		position: absolute;
		background-color: rgba(0, 0, 0, 0.5);
		transition: transform 0.1s ease;
		transform: translateX(20px) translateY(20px);
		z-index: 10;
		border-radius: 40px;
		transform-style: flat;
		pointer-events: none;
		filter: blur(5px);
	}

	.sidebar h1 {
		margin-top: 35px;
		margin-bottom: 35px;
		padding: 0px;
		color: rgb(25, 6, 68);
		font-size: 4.5rem;
		font-family: 'Abril Fatface', serif;
		font-weight: 700;
	}

	.sidebar nav ul {
		list-style-type: none;
		padding: 0;
		margin: 0;
	}

	.sidebar nav ul li {
		margin: 10px 0;
	}

	.sidebar nav ul li a {
		text-decoration: none;
		color: #838196;
		font-size: 1.3rem;
		font-weight: bold;
		padding: 10px 15px;
		display: block;

		border-radius: 15px;
		transition:
			background-color 0.1s ease,
			color 0.1s ease;
	}

	.sidebar nav ul li a:hover {
		background-color: #d5dee5;
		color: #161616;
	}

	@media (max-width: 1000px) {
		.sidebar-container {
			position: fixed;
			top: 0;
			margin: 0px;
			z-index: 10;
		}
		.sidebar {
			position: relative;
			top: 0px;
			height: max-content;
			min-width: 150px;
			transition: left 0.3s ease;

			left: -140px;
			margin: px;
			margin-right: -50px;
			margin-left: 0px;

			padding: 0px;
			padding-left: 0px;
			border-top-left-radius: 0px;
			border-top-right-radius: 0px;

			border-bottom-left-radius: 0px;

			box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
			text-align: left;
			background-color: rgb(255, 255, 255);
			padding: 10px;
		}

		.shadow {
			background-color: rgba(0, 0, 0, 0.15);
			transform: translateX(0px) translateY(15px);
			filter: blur(5px);
			left: -140px;
			transition: left 0.3s ease;
		}

		.sidebar nav ul li a {
			display: block;
			border-radius: 15px;
			transition:
				background-color 0.1s ease,
				color 0.1s ease;
		}
		.sidebar.open {
			left: 0px; /* Move the sidebar into view */
		}
		.shadow.open {
			left: 0px; /* Move the sidebar into view */
		}

		.sidebar h1 {
			display: none;
			padding: 0;
			margin: 0;
			font-size: 0.1rem; /* Increase font size for emphasis */
		}
	}
</style>
