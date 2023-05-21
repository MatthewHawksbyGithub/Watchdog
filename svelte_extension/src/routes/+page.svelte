<script lang="ts">
    import Divider from "./Divider.svelte";

    const apiRoute = "https://watchdog-iota.vercel.app/api/gpt/scam"
    let url: string;

    let text = ""

    let response = ""

    async function askGPT(){
        fetch(apiRoute, {
            mode: 'cors',
            method:"POST",
            body: JSON.stringify({
                prompt: "Check if there are anything scam related in the following text." + text
            })
        }).then(res=>{console.log(res); return res.text();}).then(
            txt => response = txt
        )
    }
</script>

<div class="container">
    <div class="title">Watchdog</div>
    <div class="text-line">Enter suspicious text here</div>
    <textarea class="text-box" rows="4"></textarea>
    <a href="#" class="button">Submit</a>
</div>

<!--
<div class="container">
    <div class="title">Watchdog</div>
    <div class="text-line">Enter suspicious text here</div>
    <textarea class="text-box" placeholder = "woof woof" rows="4" bind:value={text}></textarea>
    <button on:click={askGPT}>GO</button>

    {#if response}
    <Divider/>
    GPT Response:
    <p>{response}</p>

    {:else}
    Nothing here yet.

    {/if}
</div>

    <title>Watchdog</title>
-->
<style>
    /* CSS styles */
    body {
    font-family: Arial, sans-serif;
    }

    .container {
    background-color: #ffffff;
    border-radius: 10px;
    padding: 20px;
    width: 400px;
    margin: 0 auto;
    }

    .title {
    font-size: 24px;
    text-align: center;
    margin-bottom: 20px;
    }

    .text-line {
    font-size: 12px;
    text-align: center;
    margin-bottom: 10px;
    }

    .text-box {
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-bottom: 20px;
    }

    .button {
    display: block;
    width: 120px;
    height: 40px;
    background-color: #007bff;
    color: #fff;
    text-align: center;
    line-height: 40px;
    text-decoration: none;
    border-radius: 5px;
    margin-left: auto;
    }
</style>
