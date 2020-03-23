<script>

    // EXPORT
    export let LINK;

    // IMPORT
    import CustomRow from './CustomRow.svelte'
    import SmartCell from './SmartCell.svelte'

    // VARIABLES
    let lines = []
    let tableHeader = []
    let datas = []
    let categories = []
    let selectedCategory;

    // FUNCTIONS
    function camelize(str) {
        return str.replace(/(?:^\w|[A-Z]|\b\w)/g, function(word, index) {
            return index === 0 ? word.toLowerCase() : word.toUpperCase();
        }).replace(/\s+/g, '');
    }
    function resetFilters() {
        selectedCategory = ""
    }

    // create xhr
    var xhr = new XMLHttpRequest()

    // get a callback when the server responds
    xhr.addEventListener('load', () => {
        // update the state of the component with the result here
        lines = xhr.responseText.split("\n")

        // prendo l'header
        tableHeader = lines[0].split("\t")
        lines = lines.splice(1)

        // ciclo tutti gli elementi, tranne l'header
        for (let i = 0; i < lines.length; i++) {
            const line = lines[i].split("\t");

            let obj = {
                key: i,
            }

            for (let i2 = 0; i2 < tableHeader.length; i2++) {
                const nomeColonna = tableHeader[i2];
                
                obj[camelize(nomeColonna)] = line[i2]

            }
            
            datas = [...datas, obj]

            if (!categories.includes(obj.categoria)) {
                categories = [...categories, obj.categoria]
            }
            
        }

    })
    
    // open the request with the verb and the url
    xhr.open('GET', LINK, data => {
        console.log(lines.length);
    })
    // send the request
    xhr.send()


</script>

<div>

    <div id="filtraCategorieContainer">
    Filtra per categoria:
    <select bind:value={selectedCategory}>
            <option value="">Tutte le categorie</option>
        {#each categories as categoria}
			<option value={categoria}>
				{categoria}
			</option>
		{/each}
    </select>
    {#if selectedCategory}
    <button on:click={resetFilters}>Annulla filtri</button>
    {/if}
    </div>

    <table>
        <!-- stampo l'intestazione  -->
        <tr>
            {#each tableHeader as headerElement}
                <th>{headerElement}</th>
            {/each}
        </tr>

        <!-- simple rows -->
        {#each lines.filter( e => {return selectedCategory ? e.split("\t")[2] == selectedCategory : true} ) as line}
        <tr>
            {#each line.split("\t") as cell}
                <SmartCell text={cell} />
            {/each}
        </tr>
        {/each}

        <!-- custom rows  -->
        <!-- {#each datas as data}
            <CustomRow {data} />
        {/each} -->

    </table>

</div>

<style>
    #filtraCategorieContainer, #filtraCategorieContainer > select {
        font-size: 20px;
    }
    #filtraCategorieContainer {
        float: left;
        padding: 15px;
        border: 1px solid lightgray;
        border-radius: 6px;
        margin-bottom: 20px;
    }
</style>