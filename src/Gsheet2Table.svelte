<script>

    // EXPORT
    export let LINK;

    // VARIABLES
    let lines = []
    let tableHeader = []
    let datas = {}

    // FUNCTIONS
    function line2object(line) {
        
    }

    // create xhr
    var xhr = new XMLHttpRequest()

    // get a callback when the server responds
    xhr.addEventListener('load', () => {
        // update the state of the component with the result here
        lines = xhr.responseText.split("\n")

        // prendo l'header
        tableHeader = lines[0].split("\t")

        datas = lines

    })
    
    // open the request with the verb and the url
    xhr.open('GET', LINK, data => {
        console.log(lines.length);
    })
    // send the request
    xhr.send()


</script>

<div>
    <table>
        <!-- stampo l'intestazione  -->
        <tr>
            {#each tableHeader as headerElement}
                <th>{headerElement}</th>
            {/each}
        </tr>

        <!-- stampo il resto delle colonne  -->
        {#each lines as line}
        <tr>
            {#each line.split("\t") as cell}
                <td>{cell}</td>
            {/each}
        </tr>
        {/each}

    </table>

</div>