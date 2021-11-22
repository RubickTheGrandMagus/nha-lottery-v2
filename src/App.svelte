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
				<summary class="is-size-3">
					PARTICIPANTS
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
				<summary class="is-size-3">
					AVAILABLE HOUSING UNITS
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
			<button class="is-large button is-success is-rounded">Generate &nbsp;<span class="zap">⚡</span></button>
		</div>
	</div>
</div>

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
</style>

<script>
	  let peers = []
	  let housing = []
	  let inputPeer = ''
	  let inputNHA = ''
	  let SubDiv = "Enter Housing Subdivision"

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
			peers = [...peers, element.replace(/^\s+|\s+$/gm,'')]
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
</script>