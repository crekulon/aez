---
---
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8">
	<link href="./styles.css" rel="stylesheet"> 
</head>

<body>
	<main>
		<div class="section-container ooc" id="z1">
			<div class="tab">OOC</div>
			<section>
				<div class="sec-header">
					<div>
						<img src="./img/uldah.png">
						<p>Trading<br>Worldwide<br>Foreva</p>
					</div>
					<h2>
						East Aldenard Trading Company
						<span>Employee 3814 Information</span>
					</h2>
					<div>
						<p>Ul'Dah Office Four</p>
						<p>Steps of Bald</p>
						<p>In da alley</p>
					</div>
				</div>
				{{ site.data.ooc.ooc | markdownify}}
			</section>
		</div>
		<div class="section-container" id="z2">
			<div class="tab">Media</div>
			<section>
				<div class="sec-header">
					<div>
						<img src="./img/uldah.png">
						<p>Trading<br>Worldwide<br>Foreva</p>
					</div>
					<h2>
						East Aldenard Trading Company
						<span>Employee 3814 Information</span>
					</h2>
					<div>
						<p>Ul'Dah Office Four</p>
						<p>Steps of Bald</p>
						<p>In da alley</p>
					</div>
				</div>

				<div class="media">
					{% for media in site.media %}
						<div style="background-image: url({{ media['image'] }})"></div>
					{% endfor %}
				</div>
			</section>
		</div>
		<div class="section-container" id="z3">
			<div class="tab">Hooks</div>
			<section>
				<div class="sec-header">
					<div>
						<img src="./img/uldah.png">
						<p>Trading<br>Worldwide<br>Foreva</p>
					</div>
					<h2>
						East Aldenard Trading Company
						<span>Employee 3814 Information</span>
					</h2>
					<div>
						<p>Ul'Dah Office Four</p>
						<p>Steps of Bald</p>
						<p>In da alley</p>
					</div>
				</div>

				<div class="sec-content">
					<h2>Employee Services</h2>
					{% for hook in site.hooks %}
						<div class="hook">
							<h3>{{ hook.title }}</h3>
							{{ hook.content | markdownify | replace: " ", " "}}
						</div>
					{% endfor %}
				</div>
			</section>
		</div>
		<div class="section-container topmost-page" id="z4">
			<div class="tab">Bio</div>
			<section>
				<div class="sec-header">
					<div>
						<img src="./img/uldah.png">
						<p>Trading<br>Worldwide<br>Foreva</p>
					</div>
					<h2>
						East Aldenard Trading Company
						<span>Employee 3814 Information</span>
					</h2>
					<div>
						<p>Ul'Dah Office Four</p>
						<p>Steps of Bald</p>
						<p>In da alley</p>
					</div>
				</div>

				<div class="sec-content">
					<h2>Employee Details</h2>
					<div class="stats">
						{{ site.data.bio.biostats | markdownify | replace: " ", " " }}
						<div class="portait"></div>
					</div>
					
					{{ site.data.bio.bio | markdownify | replace: " ", " " }}
				</div>
			</section>
		</div>
	</main>

	<script>
		var sections = document.querySelectorAll(".section-container");
		for (var i = 0; i < sections.length; i++) {
			var current = sections[i];
			current.addEventListener('click', function (event) {
				console.log(this);	
			}, false);
		}

		var tabs = document.querySelectorAll(".tab");
		for (var i = 0; i < tabs.length; i++) {
			var current = tabs[i];

			current.addEventListener('mouseenter', function (event) {
				document.body.classList.add('hovering-section');
				this.parentNode.classList.add('hovered-section');
			}, false);

			current.addEventListener('mouseleave', function (event) {
				document.body.classList.remove('hovering-section');
				this.parentNode.classList.remove('hovered-section');
			}, false);

			current.addEventListener('click', function (event) {
				document.body.classList.add('transitioning-page');
				this.parentNode.classList.add('transitioned-page')
				
				setTimeout(() => {
					let formerTop = document.getElementsByClassName('topmost-page');
					while(formerTop.length > 0) {
						let previousTop = document.getElementsByClassName('previous-page');
						while(previousTop.length > 0) {
							previousTop[0].classList.remove('previous-page');
						}

						formerTop[0].classList.add('previous-page');
						formerTop[0].classList.remove('topmost-page');
					}
					this.parentNode.classList.add('topmost-page');

					document.body.classList.remove('transitioning-page');					
					this.parentNode.classList.remove('transitioned-page')

					document.body.classList.add('transitioning-in');
					setTimeout(() => {
						document.body.classList.remove('transitioning-in');					
					}, 600);
				}, 800);
			}, false);
		}

		//no idea why but netlify has an encoding problem
		var re = new RegExp(String.fromCharCode(160), "g");
		document.querySelectorAll('.sec-content p').forEach(p => {
			p.textContent = p.textContent.replace(re, " ")
		});


	</script>
</body>
</html>