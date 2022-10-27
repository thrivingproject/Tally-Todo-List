<script>
	let count = {}
	let tallies = []
	let tallyText = ''

	function increment(e) {
		let id = e.target.id;
  	    count[id]++;
	}
	
	function add() {
        if (tallyText !== '') {
		tallies = [...tallies, tallyText]
		count[tallyText] = 1
		tallyText = ''
    }
	}
	
	function reset() {
		tallies = []
		count = {}
		tallyText = ''
	}

    function decrement(e) {
        let id = e.target.id
        if (count[id] > 0) {
            count[id]--
        }
    }
</script>

<main>
    <h1>
        Tally App
    </h1>

    <section class=menu>
        <form on:submit|preventDefault={add}>
            <input bind:value={tallyText} placeholder='Request'>
            <input class=button type=button value='add' on:click={add}>
        </form>
        <button on:click={reset}>
            reset
        </button>
    </section>

    <ul>
        {#each tallies as tally}
        <section class=tally>
            <h3>{tally}</h3>
            <div class=tallier>
                <button on:click={decrement} id={tally}>-</button>
                <p>{count[tally]}</p>
                <button on:click={increment} id={tally}>+</button>
            </div>
        </section>
        {/each}
    </ul>
</main>

<style>
    * {
        box-sizing: border-box;
        margin: 0;
    }
    main {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 75vw;
        margin: auto;
    }
	section button, .button {
		padding: .5rem 1.5rem;
	}
    .tallier button {
        padding: .5rem 1rem;
    }
	form, .menu, .tallier {
		display: flex;
		column-gap: 1rem;
	}
    .tallier {
        align-items: center;
    }
	ul {
		display: flex;
		flex-direction: column;
		padding: 0 1rem;
        row-gap: .25rem;
        width: 100%;
	}
	.tally {
		display: flex;
		justify-content: space-between;
	}
    h1, .menu {
        margin-bottom: 2.5rem;
    }
</style>