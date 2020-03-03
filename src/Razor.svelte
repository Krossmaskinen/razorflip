<script>
    let noOfFlipsRemaining = 1;
    let noOfUsesOnCurrentSideRemaining = 3;
    let usable = true;

    function flip() {
        noOfFlipsRemaining -= 1;
        noOfUsesOnCurrentSideRemaining = 3;
    }

    function use() {
        noOfUsesOnCurrentSideRemaining -= 1;
    }

    function disable() {
        usable = false;
    }

    function updateState() {
        if (noOfUsesOnCurrentSideRemaining < 1) {
            if (noOfFlipsRemaining > 0)
                flip();
            else
                disable();
        }
    }

    function shave() {
        use();
        updateState();
    }
</script>

<div>
    <h3>My razor</h3>
    {#if usable}
        <button on:click={shave}>Shave</button>
    {:else}
        <div>This razor is trash. Put on a new one!</div>
    {/if}

    <div>Uses remaining on this side: {noOfUsesOnCurrentSideRemaining}</div>
    <div>Flips remaining: {noOfFlipsRemaining}</div>
</div>