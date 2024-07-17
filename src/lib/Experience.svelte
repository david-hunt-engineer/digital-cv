<script>
	export let experiences = [
		{
			role: 'Contracting: Data Scientist',
			company: 'Ingenum',
			duration: '2024 – Present',
			image: '/assets/ingenum_logo.png',
			description: `
			Applying deep learning methods to detect emerging signs of livestock disease.
			Managing national scale weather dataset
			Deploying development environments for analysis team
		`,
		},
		{
			role: 'Contracting: Data Scientist',
			company: 'Black Pearl Group',
			duration: '2022 – Present',
			image: '/assets/bp_logo.png',
			description: `
			Co-leading design and implementation of data transformation pipeline with Snowflake and Azure Data Factory.
		    Advising on AI maturity of a business during a potential merger/acquisition.
		    Scoping, design, and delivering an AI solution for detecting Humans/Bots in email activity data.
		`,
		},
		{
			role: 'Contracting: Data Scientist & Data Consultant',
			company: 'Litmus Datatech',
			duration: '2021 – Present',
			image: '/assets/litmus_logo.png',
			description: `
			Developed geospatial data pipeline for Eco-index's novel data products.
		    Advising on and implementing data strategy and fundamentals.
		    Diagnosing faults in an industrial process based on time series data.
		    Delivering pragmatic insights and bespoke analysis for various NZ businesses.
		`,
		},
		{
			role: 'Senior Data Scientist + Pod Lead',
			company: 'Qrious',
			duration: '2020 – 2022',
			image: '/assets/qrious_logo.png',
			description: `
		    Implementing a real-time cloud hosted hazard detection solution using computer vision.
		    Leading the development of machine learning models for conservation and healthcare.
		    Providing AI-related strategy, education, and recommendations for multiple clients.
		`,
		},
		{
			role: 'Data Scientist / AI Engineer',
			company: 'Xero',
			duration: '2017 – 2020',
			image: '/assets/xero_logo.png',
			description: `
		    Applying Bayesian modeling and ML techniques to accounting data.
		    Creating bespoke interactive data visualizations.
		    Building ML models for text, image, and free-text data analysis.
		`,
		},
		{
			role: 'Data Visualisation Contract',
			company: 'CrowdReader',
			duration: '2019',
			image: '/assets/crowdreader_logo.png',
			description: `
			Creating and iterating on D3 data visualisation concepts with client to converge on a great solution.
			Integrating D3 visualisation code into web application for use in production.
			`,
		},
		{
			role: 'Developer',
			company: 'FNZ',
			duration: '2016 – 2017',
			image: '/assets/fnz_logo.png',
			description: `
			Working with SQL Server to extract data and generate reports for compliance purposes.
			Developing in C# on multiple large code bases.
			`,
		},
	];
</script>

<h2>Work Experience</h2>

<div class="experience">
	{#each experiences as experience}
		<div class="job job-hover-effect">
			<div class="job-left">
				{#if experience.image}
					<img
						src={experience.image}
						alt={experience.company + ' logo'}
						class={experience.company.toLowerCase().replace(/\s/g, '-') + '-logo'}
					/>
				{/if}
				<div class="duration {experience.duration.includes('Present') ? 'current-experience' : ''}">
					{experience.duration}
				</div>
			</div>
			<div class="job-right">
				<h3>{experience.role}</h3>
				<!-- <p>{experience.company}</p> -->
				<div class="description">
					<ul>
						{#each experience.description
							.trim()
							.split('\n')
							.filter((line) => line.trim()) as desc}
							<li>{desc.trim()}</li>
						{/each}
					</ul>
				</div>
			</div>
		</div>
	{/each}
</div>

<style>
	.experience {
		margin: 0px;

		/* margin-bottom: -30px; */
		border-radius: 30px;
		padding: 15px 15px 0px 15px;
		box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
		background-color: #fff;
		border: 1px solid #ddd;
	}
	.job {
		display: flex;
		align-items: flex-start;
		padding: 10px;
		margin: 10px 0px 15px 0px;
		flex-direction: row;
		transition: transform 0.3s;
	}
	.job-hover-effect {
		background-color: rgba(255, 255, 255, 1);
		margin-top: -1px;
		/* margin-left: -1.5px; */
		border: 3px solid rgba(125, 103, 103, 0);
		border-radius: 20px;
		box-shadow: 5px 5px 5px 0px rgba(107, 107, 107, 0);
		transition:
			border 500ms ease,
			box-shadow 1000ms ease;

		&:hover {
			border: 3px solid rgba(125, 103, 103, 0.1);
			/* background-color: rgba(255, 255, 255, 1); */
			box-shadow: 5px 5px 15px 0px rgba(107, 107, 107, 0.1);
			transition: None;
		}
	}

	.job-left {
		flex: 0 0 25%; /* Fixed width for the left column */
		text-align: center;
		padding-right: 0px;
	}

	.job-left img {
		max-width: 100px; /* Max width for the image */
		margin-bottom: 10px;
	}

	.job-left .duration {
		font-weight: light;
		color: #666;
	}

	.job-right {
		flex: 1;
	}

	.job-right h3 {
		margin: 0;
		font-size: 1.2rem;
		font-weight: bold;
	}

	.job-right .description {
		margin-top: 10px;
	}

	.job-right .description ul {
		list-style-type: disc; /* Use disc for rounded bullets */
		padding-left: 20px; /* Indent the list */
	}

	.job-right .description li {
		margin-bottom: 5px; /* Space between list items */
	}
	.current-experience {
		animation: colorChange 2s infinite alternate; /* Apply the animation */
	}

	@keyframes colorChange {
		0% {
			color: #343434;
		}
		50% {
			color: #48764d;
		}
		100% {
			color: #5ed354;
		}
	}

	/* Adding black background to Ingenum logo */
	.ingenum-logo {
		background-color: rgb(139, 139, 139);
		border-radius: 10px;
		padding: 5px; /* Add some padding to separate the image from the edges */
	}

	@media (max-width: 1000px) {
		.experience {
			margin-top: 0px;
			margin-bottom: 30px;
			margin-left: 0px;
			margin-right: 0px;
			padding: 8px;
			box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
			background-color: #fff;
			border: 1px solid #ddd;
		}

		.job-left {
			align-items: center;
			padding-right: 0; /* Remove right padding */
			margin-bottom: 20px; /* Add some space below the image and duration */
		}

		.job-right {
			text-align: left; /* Align text to left for readability */
			margin-bottom: 20px; /* Add some space below the image and duration */
			margin-right: 0px;
			padding: 4px;
		}

		.job-right {
			flex: 1;
		}

		.job-right h3 {
			margin: 0;
			font-size: 1.2rem;
			font-weight: bold;
		}

		.job-right p li {
			margin: 5px 0;
			font-weight: bold;
			color: #333;
			font-size: 0.8rem;
		}

		.job-right .description {
			margin-top: 10px;
		}

		.job-right .description ul {
			list-style-type: disc; /* Use disc for rounded bullets */
			padding-left: -5px; /* Indent the list */
		}

		.job-right .description li {
			margin-bottom: 5px; /* Space between list items */
		}
		.current-experience {
			animation: colorChange 2s infinite alternate; /* Apply the animation */
		}
	}
</style>
