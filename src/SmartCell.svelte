<script>
    export let text;
    let linkRegex = /https?:\/\/(www\.)?[-a-zA-Z0-9@:%._\+~#=]{2,256}\.[a-z]{2,4}\b([-a-zA-Z0-9@:%_\+.~#?&//=]*)/

    // is it a link?
    if ( text.match(linkRegex) ) {
        text = "<a>"+text+"</a>"
    } else {
        // text = ""
    }

</script>

<td>
    <!-- Controllo se è un link -->
    {#if text.match(linkRegex)}
        <a href={text}>Link</a>
    {:else}
        {text}
    {/if}
</td>