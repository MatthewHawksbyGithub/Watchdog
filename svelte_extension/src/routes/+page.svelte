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
            txt =>{
                response = txt;
                console.log(response);
            }

        )
    }
</script>

<div class="container">
    <div class="text-line">Watch out for suspicious stuff with</div>
    <div class="title">Watchdog</div>
    <div class="text-line2">Enter suspicious text here</div>
    <textarea class="text-box" rows="4" bind:value={text}></textarea>
    <button class="button" on:click={askGPT}>Analyse Text</button>

    {#if response}
    <Divider/>
    GPT Response:
    <p>{response}</p>

    {:else}

    {/if}
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
    @import url("https://fonts.googleapis.com/css2?family=DM+Mono:ital,wght@0,300;0,400;0,500;1,300;1,400;1,500&family=Manrope:wght@200;300;400;500;600;700;800&display=swap");

    .container {
    
    font-family: Arial, sans-serif;
    background-color: #807e7e;
    font-size: 12px;
    border-radius: 10px;
    padding: 20px;
    width: 400px;
    margin: 0 auto;
    margin-left: 10px;
    }
    .title{
        font-size: 36px;
        
    }

    .text-line {
    font-family: Manrope, sans-serif;
    font-size: 16px;
    text-align: left;
    margin-bottom: 10px;
    margin-left:0px;
    }

    .text-line2 {
    font-size: 16px;
    text-align: left;
    margin-bottom: 10px;
    margin-left:5px;
    }

    .text-box {
    width: 90%;
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
    font-size: 16px;
    
    font-family: Manrope, sans-serif;
    }
</style>
