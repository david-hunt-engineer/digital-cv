<script>
	export let projects = [
		{
			title: 'Coming soon..',
			description: '',
			link: '#',
			tags: ['AI', 'Analytics'],
		},
	];
</script>

<div class="projects">
	<h2>Projects</h2>

	{#each projects as project}
		<div class="project">
			<h3><a href={project.link}>{project.title}</a></h3>
			<p>{project.description}</p>
			<div class="tags">
				{#each project.tags as tag}
					<span class="tag">{tag}</span>
				{/each}
			</div>
		</div>
	{/each}
</div>

<style>
	.projects {
		display: grid;
		gap: 20px;
	}
	.project {
		border-radius: 30px;
		padding: 20px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		background-color: #fff;
		border: 1px solid #ddd;
		transition: transform 0.3s;
	}

	.project:hover {
		transform: translateY(-5px);
	}

	.project h3 {
		margin-top: 0;
	}

	.project p {
		color: #555;
	}

	.tags {
		margin-top: 10px;
		padding-left: 20px;

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
</style>
