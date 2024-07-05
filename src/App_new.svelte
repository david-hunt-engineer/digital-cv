<script>
	import About from './routes/About.svelte';
	import Experience from './routes/Experience.svelte';
	import Projects from './routes/Projects.svelte';
</script>

<div class="container">
	<aside class="sidebar">
		<h2>David Hunt</h2>
		<p>Senior Data Scientist & AI Specialist</p>
		<nav>
			<ul>
				<li><a href="#about">About</a></li>
				<li><a href="#experience">Experience</a></li>
				<li><a href="#projects">Projects</a></li>
			</ul>
		</nav>
	</aside>

	<main class="content">
		<section id="about">
			<About />
		</section>

		<section id="experience">
			<Experience />
		</section>

		<section id="projects">
			<Projects />
		</section>
	</main>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap');

	body {
		font-family: 'Poppins', sans-serif;
		color: #333;
		background-color: #f4f4f4;
		margin: 0;
		padding: 0;
	}

	.container {
		display: flex;
		max-width: 1200px;
		margin: 50px auto;
		padding: 5% 10%;
	}

	.sidebar {
		flex: 0 0 250px;
		margin-right: 20px;
		background-color: #fff;
		border-radius: 15px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		padding: 30px;
		text-align: center; /* Center the text */
	}

	.sidebar h2 {
		margin-top: 0;
		font-weight: 600;
		color: #2c3e50;
		font-size: 1.5rem;
	}

	.sidebar p {
		color: #7f8c8d;
		margin-bottom: 20px;
	}

	.sidebar nav ul {
		list-style-type: none;
		padding: 0;
		margin: 0;
	}

	.sidebar nav ul li {
		margin: 15px 0;
	}

	.sidebar nav ul li a {
		text-decoration: none;
		color: #2980b9;
		font-weight: 500;
		transition: color 0.3s;
	}

	.sidebar nav ul li a:hover {
		color: #3498db;
	}

	.content {
		flex: 1;
		background-color: #fff;
		border-radius: 15px;
		padding: 30px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
	}

	.project-box {
		background-color: #fff;
		border-radius: 10px;
		padding: 15px;
		margin-bottom: 20px;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	}

	.tags {
		margin-top: 10px;
		display: flex;
		flex-wrap: wrap;
		gap: 10px;
	}

	.tag {
		background-color: #f0f0f0;
		padding: 5px 10px;
		border-radius: 15px;
		font-size: 0.8rem;
		color: #333;
	}

	@media (max-width: 768px) {
		.container {
			flex-direction: column;
			padding: 5%;
		}

		.sidebar {
			flex: none;
			margin-right: 0;
			margin-bottom: 20px;
		}

		.content {
			padding: 20px;
		}
	}
</style>
