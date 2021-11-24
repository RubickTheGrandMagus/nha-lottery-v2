<div class="container is-max-desktop">
	<div class="notification is-primary has-text-centered ">
		<p>
			<span class="b-icon icon is-size-1 has-text-danger">
				<i class="fa fa-home" aria-hidden="true"></i>
			</span>
			<span class="has-text-weight-bold is-size-1 px-6">NHA Lottery</span>
			<span class="b-icon icon is-size-1 has-text-warning">
				<i class="fa fa-trophy" aria-hidden="true"></i>
			</span>
		</p>
		<p class="nha-subdiv">
			<input class="input" type="text" bind:value={SubDiv} placeholder="Enter Housing Subdivision">
			<span class="has-text-weight-bold is-size-1">{SubDiv}</span>
		</p>
	</div>
	<hr>
	<div class="columns">
		<div class="column">
			<details>
				<summary class="is-size-3 has-text-centered">
					PARTICIPANTS ({peers.length})
				</summary>
				<div class="content">
					<div class="field is-grouped">
						<p class="control is-expanded"><input bind:value={inputPeer} type="text" class="input" placeholder="Enter participant" on:keypress={e=>addParticipants(e)}></p>
						<p class="control"><button class="button is-primary" on:click={()=>addParticipants(inputPeer,true)}><span class="icon is-small"><i class="fa fa-reply" aria-hidden="true"></i></span></button></p>
					</div>
					<ol>
						{#each peers as item,i}
							<li><code>{item}</code><span class="icon is-small" on:click={()=>deleteParticipants(i)}><i class="fa fa-trash" aria-hidden="true"></i></span></li>
						{/each}
					</ol>
				</div>
			</details>
		</div>
		<div class="column">
			<details>
				<summary class="is-size-3 has-text-centered">
					AVAILABLE HOUSING UNITS ({housing.length})
				</summary>
				<div class="content">
					<div class="field is-grouped">
						<p class="control is-expanded"><input bind:value={inputNHA} type="text" class="input" placeholder="Enter Housing Unit" on:keypress={e=>addNHA(e)}></p>
						<p class="control"><button class="button is-primary" on:click={()=>addNHA(inputNHA,true)}><span class="icon is-small"><i class="fa fa-reply" aria-hidden="true"></i></span></button></p>
					</div>
					<ol>
						{#each housing as item,i}
							<li><code>{item}</code><span class="icon is-small" on:click={()=>deleteNHA(i)}><i class="fa fa-trash" aria-hidden="true"></i></span></li>
						{/each}
					</ol>
				</div>
			</details>
		</div>
	</div>
	<hr>
	<div class="columns">
		<div class="column has-text-centered">
			{#if output.length==housing.length}
				<button class="is-large button is-info is-rounded">Print Result &nbsp; 🖨️</button>
			{:else}
				<button class="is-large button is-success is-rounded" on:click={()=>modal=generate()}>Generate &nbsp;<span class="zap">⚡</span></button>
			{/if}
			<button class="is-large button is-danger is-rounded" on:click={()=>{winners=[];output=[]}}><span class="icon is-small xrotate"><i class="fa fa-history"  aria-hidden="true"></i></span></button>
		</div>
	</div>
	<div class="columns">
		<div class="column has-text-centered">
			{#each output as item}
				<div class="notification is-info is-size-2">{item}</div>
			{/each}
		</div>
	</div>
	{#if modal}
	<div class="modal is-active" in:scale={{duration:2000}}>
		<div class="modal-background"></div>
		<div class="modal-content box has-text-centered is-size-1 has-text-weight-bold">
			<p in:spin={{duration:20000}}>
				<span class="winner icon has-text-warning">🌟</span> &nbsp;{congrats.winner} &nbsp;<span class="winner icon has-text-warning">🌟</span>
			</p>
			<p>
				<span class="b-icon icon is-size-1 has-text-danger">
					<i class="fa fa-home" aria-hidden="true"></i>
				</span>
				{congrats.housing}
				<span class="b-icon icon is-size-1 has-text-danger">
					<i class="fa fa-home" aria-hidden="true"></i>
				</span>
			</p>
		</div>
		<button class="modal-close is-large" aria-label="close" on:click={()=>modal=false}></button>
	  </div>
	  {/if}
	</div>
	{#if modal}
			{#each confetti as c}
				<span class="props" style="left: {c.x}%; top: {c.y}%; transform: scale({c.r})" out:fade>{c.character}</span>
			{/each}
	{/if}

<style>
	  .nha-subdiv:hover>span{
		  display:none;
	  }
	  .nha-subdiv>input{
		  display:none
	  }
	  .nha-subdiv:hover>input{
		  display: block;
	  }
	  summary,.fa-trash{cursor: pointer}
	  .fa-trash:hover{color:red}
	  .b-icon{
		animation:example 2s linear infinite;
	  }
	  @keyframes example{
			from{
				transform:rotateY(0deg)
			}
			to{
				transform:rotateY(360deg)
			}
		}
	button:hover>span.zap{
		animation: shake 0.5s infinite;
	}
	@keyframes shake{
		0% { transform: translate(1px, 1px) rotate(0deg); }
		10% { transform: translate(-1px, -2px) rotate(-1deg); }
		20% { transform: translate(-3px, 0px) rotate(1deg); }
		30% { transform: translate(3px, 2px) rotate(0deg); }
		40% { transform: translate(1px, -1px) rotate(1deg); }
		50% { transform: translate(-1px, 2px) rotate(-1deg); }
		60% { transform: translate(-3px, 1px) rotate(0deg); }
		70% { transform: translate(3px, 1px) rotate(-1deg); }
		80% { transform: translate(-1px, -1px) rotate(1deg); }
		90% { transform: translate(1px, 2px) rotate(0deg); }
		100% { transform: translate(1px, -2px) rotate(-1deg); }
	}
	.winner{
		animation: rubberBand 1s infinite;
		text-shadow: 2px 2px black;
	}

	@keyframes rubberBand {
		from {transform: scale3d(1, 1, 1)}
		30% {transform: scale3d(1.25, 0.75, 1)}
		40% {transform: scale3d(0.75, 1.25, 1)}
		50% {transform: scale3d(1.15, 0.85, 1)}
		65% {transform: scale3d(.95, 1.05, 1)}
		75% {transform: scale3d(1.05, .95, 1)}
		to {transform: scale3d(1, 1, 1)}
	}

	.props{ position:absolute;font-size:5vw;user-select: none;}

	.xrotate:hover{
		animation: rotate 2s linear infinite;
	}
	@keyframes rotate{
		100%{ transform: rotate(-360deg);}
	}
	.modal-background{background-color:bisque;opacity:0.2}
	.box{border:5px dotted grey; overflow: hidden;}
</style>

<script>
	  import {fade,scale} from 'svelte/transition'
	  import {elasticOut} from 'svelte/easing'
	  import {onMount} from 'svelte'

	  let peers = []
	  let housing = []
	  let winners = []
	  let output = []
	  let reserved = []
	  let congrats = {winner:'',housing:''}
	  let inputPeer = ''
	  let inputNHA = ''
	  let SubDiv = "Enter Housing Subdivision"
	  let modal = false

	  function addParticipants(e,d=false){ //d is true when using the submit button
		let peer = (typeof e ==='object')? e.target.value:e
		
		if(e.key === "Enter" || d){

			if(peer.search('/')>=0) return bacthEntryParticipants(peer)
		
			if(!peer || peer.length<7) return alert("Must be not less than 7 characters!")

			peers = [...peers, peer]

			inputPeer=""

			if(d) return  //don't continue if submit button is pressed
			e.target.value = ""
		}
	  }

	  function deleteParticipants(e){
		  peers = peers.filter((t,i)=>i!==e) //filter array using index givin
	  }

	  function bacthEntryParticipants(e){
		let rawList = e.split('/').filter(t=> t.length>7)
		rawList.forEach(element => {
			let limpyo = element.replace(/^\s+|\s+$/gm,'')
			peers = [...peers, limpyo.replace(/\*/g,'')]
			let marker = (!element.match(/\*/g))? 0:element.match(/\*/g).length
			if(marker > 0){ reserved = [...reserved,{index:marker-1,data:limpyo.replace(/\*/g,'')}] }
		});
		inputPeer="" //reset inputPeer
	  }

	  function addNHA(e,d=false){ //d is true when using the submit button
		let unit = (typeof e ==='object')? e.target.value:e
		
		if(e.key === "Enter" || d){

			if(unit.search('/')>=0) return bacthEntryNHA(unit)
		
			if(!unit || unit.length<7) return alert("Must be not less than 7 characters!")

			housing = [...housing, unit]

			inputNHA=""

			if(d) return  //don't continue if submit button is pressed
			e.target.value = ""
		}
	  }

	  function deleteNHA(e){
		  housing = housing.filter((t,i)=>i!==e) //filter array using index givin
	  }

	  function bacthEntryNHA(e){
		let rawList = e.split('/').filter(t=> t.length>7)
		rawList.forEach(element => {
			housing = [...housing, element.replace(/^\s+|\s+$/gm,'')]
		});
		inputNHA="" //reset inputPeer
	  }

	  function generate(){
		  if(peers.length<=0) return alert("There are no participants.")
		  if(housing.length<=0) return alert("There are no housing units.")
		
		  //Generate winner list 
		  if(winners.length<housing.length){
			let nlist = peers
			reserved.forEach(item=>nlist=nlist.filter(t=>t!=item.data))
			housing.forEach(()=>{
				const index = Math.floor(Math.random()*nlist.length)
				winners = [...winners, nlist[index]]
				nlist = nlist.filter(t=>t!=nlist[index])
			})
		  }
		  if(reserved.length>0){reserved.forEach(item=>winners[item.index]=item.data)}

		  const index = output.length

		  if(index >= housing.length) return alert("Raffle Finished")
		  output = [...output,`${housing[index]} - ${winners[index]}`]
		  congrats = {winner:winners[index],housing:housing[index]}
		  return true
	  }

	  let characters = ['🥳', '🎉', '🎈'];
	  let confetti = new Array(100).fill()
		.map((_, i) => {
			return {
				character: characters[i % characters.length],
				x: Math.random() * 100,
				y: -20 - Math.random() * 100,
				r: 0.1 + Math.random() * 1
			};
		})
		.sort((a, b) => a.r - b.r);
	
	onMount(() => {
		let frame;

		function loop() {
			frame = requestAnimationFrame(loop);

			confetti = confetti.map(emoji => {
				emoji.y += 0.7 * emoji.r;
				if (emoji.y > 120) emoji.y = -20;
				return emoji;
			});
		}

		loop();

		return () => cancelAnimationFrame(frame);
	});

	function spin(node, { duration }) {
		return {
			duration,
			css: t => {
				const eased = elasticOut(t);

				return `
					transform: scale(${eased}) rotateY(${eased * 1080}deg);`
			}
		}
	}
</script>