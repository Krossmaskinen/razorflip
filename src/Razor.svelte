<script>
    const USES_PER_SIDE = 3;
    const TOTAL_FLIPS = 1;
    let noOfFlipsRemaining = TOTAL_FLIPS;
    let remainingUsesOnCurrentSide = USES_PER_SIDE;
    let usable = true;

    function flip() {
        noOfFlipsRemaining -= 1;
        remainingUsesOnCurrentSide = USES_PER_SIDE;
    }

    function use() {
        remainingUsesOnCurrentSide -= 1;
    }

    function resetBlade() {
        noOfFlipsRemaining = TOTAL_FLIPS;
        remainingUsesOnCurrentSide = USES_PER_SIDE;
    }

    function updateState() {
        if (remainingUsesOnCurrentSide < 1) {
            if (noOfFlipsRemaining > 0)
                flip();
        }
    }

    function shave() {
        use();
        updateState();
    }

    $: razorbladeStateClass = () => {
        const classPrefix = 'razorblade--';
        const classModifier = remainingUsesOnCurrentSide + (noOfFlipsRemaining * USES_PER_SIDE);

        return classPrefix + classModifier;
    };

    $: usable = () => remainingUsesOnCurrentSide > 0;

    $: isTimeToFlip = () => remainingUsesOnCurrentSide === USES_PER_SIDE && noOfFlipsRemaining < 1;
</script>

<div>
    <h3>My razor</h3>
    <h2>
        {#if noOfFlipsRemaining}
            Side 1
        {:else}
            Side 2
        {/if}
    </h2>

    {#if usable()}
        <button on:click={shave}>Shave</button>
    {:else}
        <h3>This razor is trash!</h3>
        <button on:click={resetBlade}>Insert new blade</button>
    {/if}

    <div class="razorblade {razorbladeStateClass()}">
        <img class="razorblade__image" src="/images/razorblade-128x128.png" alt="razorblade"/>
    </div>

    {#if isTimeToFlip()}
        <h3>Flip!</h3>
    {/if}

    <div>Uses remaining on this side: {remainingUsesOnCurrentSide}</div>
    <div>Flips remaining: {noOfFlipsRemaining}</div>
</div>

<style>
    .razorblade {
        width: 128px;
        height: 128px;
        margin: auto;
    }

    .razorblade__image {
        width: 100%;
    }

    .razorblade--0 {
        background-color: #ff0600;
    }

    .razorblade--1 {
        background-color: #ff5400;
    }

    .razorblade--2 {
        background-color: #ffaf00;
    }

    .razorblade--3 {
        background-color: #FFF200;
    }

    .razorblade--4 {
        background-color: #b9d500;
    }

    .razorblade--5 {
        background-color: #69b500;
    }

    .razorblade--6 {
        background-color: #1E9600;
    }
</style>