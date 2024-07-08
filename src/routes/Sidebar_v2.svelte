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
		console.log('hover');

		if (windowWidth < 1000) {
			isOpen = true;
			sidebar.classList.toggle('open', isOpen);
			shadow.classList.toggle('open', isOpen);
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

	const handlePulltabClick = () => {
		// isOpen = !isOpen;
		// sidebar.classList.toggle('open', isOpen);
		// pulltab.classList.toggle('open', isOpen);

		console.log('do nothing');
	};

	const handleMouseLeave = () => {
		if (windowWidth < 1000) {
			isOpen = false;
			sidebar.classList.toggle('open', isOpen);
			shadow.classList.toggle('open', isOpen);
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

	function handleTouchEnd() {
		const diffX = endX - startX;
		const diffY = endY - startY;

		if (Math.abs(diffX) > Math.abs(diffY) && diffX > 50) {
			console.log('Swipe Right Detected');

			if (windowWidth < 1000) {
				isOpen = true;
				sidebar.classList.toggle('open', isOpen);
				shadow.classList.toggle('open', isOpen);
			}
		} else if (Math.abs(diffX) > Math.abs(diffY) && diffX < -50) {
			console.log('Swipe Left Detected');

			if (windowWidth < 1000) {
				isOpen = false;
				sidebar.classList.toggle('open', isOpen);
				shadow.classList.toggle('open', isOpen);
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
		sidebar.addEventListener('click', handlePulltabClick);

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
			sidebar.removeEventListener('click', handlePulltabClick);
			resizeObserver.disconnect();
		};
	});
</script>

<aside class="sidebar-container">
	<div bind:this={shadow} class="shadow"></div>
	<div bind:this={sidebar} class="sidebar">
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
		</nav>
	</div>
</aside>

<style>
</style>
