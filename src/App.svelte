<div class="container is-max-desktop">
	<div class="notification is-primary has-text-centered ">
		<p>
			<span class="b-icon icon is-size-1 has-text-black">
				<i class="fa fa-home" aria-hidden="true"></i>
			</span>
			<span class="has-text-weight-bold is-size-1 px-6">NHA Lottery</span>
			<span class="b-icon icon is-size-1 has-text-warning">
				<i class="fa fa-trophy" aria-hidden="true"></i>
			</span>
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
						<p class="control is-expanded"><input bind:value={input} type="text" class="input" placeholder="Enter participant" on:keypress={e=>addParticipants(e)}></p>
						<p class="control"><button class="button is-primary" on:click={()=>addParticipants(input,true)}><span class="icon is-small"><i class="fa fa-reply" aria-hidden="true"></i></span></button></p>
					</div>
					<ol>
						{#each peers as item}
							<li><code>{item}</code><span class="icon is-small" on:click={()=>deleteParticipants(item)}><i class="fa fa-trash" aria-hidden="true"></i></span></li>
						{/each}
					</ol>
				</div>
			</details>
		</div>
		<div class="column">
			<span class="is-size-3">AVAILABLE HOUSING UNITS</span>
		</div>
	</div>
	<hr>
	<div class="columns">
		<div class="column has-text-centered">
			<button class="is-large button is-success is-rounded"><span class="zap">Generate ⚡</span></button>
		</div>
	</div>
  </div>

  <style>
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
	.zap:hover{
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
	  let input = ''

	  function addParticipants(e,d=false){ //d is true when using the submit button
		let peer = (typeof e ==='object')? e.target.value:e
		
		if(e.key === "Enter" || d){
		
			if(!peer || peer.length<7) return alert("Must be not less than 7 characters!")

			peers = [...peers, peer]

			input=""

			if(d) return  //don't continue if submit button is pressed
			e.target.value = ""
		}
	  }

	  function deleteParticipants(e){
		  peers = peers.filter(t=>t!==e)
	  }
  </script>