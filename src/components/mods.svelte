<script lang="ts">
    import data from "../moddb.json"
    import * as Dialog from "$lib/components/ui/dialog";

    type Mods = {
        Name: string;
        Versions: string[];
        DownloadLinks: string[];
        Description: string;
        LogoPath: string;
        Release: string;
        Rating: number;
        Screenshots: string[];
    }
    let dialog: HTMLDialogElement;
    let currentMod = data.Mods[0]
</script>

<!-- svelte-ignore a11y-no-noninteractive-element-interactions -->
<div>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <dialog
     on:click={(e) => {
        if (e.target == dialog) {
            if (document.startViewTransition) {
                document.startViewTransition(() => {
                                dialog.close()
                }) 
            }else {
                dialog.close()
            }
        }
     }}
     class="w-1/3 h-[90%] "
     bind:this={dialog}>
        <div class="w-full h-full relative text-center  flex flex-col items-center py-2 gap-2">
            {#each currentMod.DownloadLinks.reverse() as download, i}
                <a href={download} class="block h-fit bg-purple-600 w-fit px-7 text-white font-bold text-xl rounded-xl hover:bg-purple-500 active:scale-90 transition-all hover:shadow-2xl shadow-black shadow- py-2">{currentMod.Versions[currentMod.Versions.length - i]}</a>
            {/each}
            <button class="absolute ml-auto mr-auto left-0 right-0 bottom-5 bg-red-500 w-fit p-2 px-10 rounded-lg text-white font-bold text-lg hover:bg-red-700 transition-all active:scale-90" 
            on:click={(e) => {
            if (document.startViewTransition) {
                document.startViewTransition(() => {
                                dialog.close()
                }) 
            }else {
                dialog.close()
            }
            }}
            >Close</button>
        </div>
      </dialog>
    <div class="flex bg-[wheat]/25">
        <div  class={"w-full h-[100vh] overflow-y-scroll relative grid grid-cols-3 auto-rows-max	 gap-x-2 gap-y-2 pt-3 px-5"}>
            {#each data.Mods as mod}
                <button on:click={() => {
                    if (document.startViewTransition) {
                        document.startViewTransition(() => {
                                        currentMod = mod
                        }) 
                    }else {
                        currentMod = mod
                    }
                }} class="aspect-[110/100] mod-selector flex items-center justify-center hover:bg-gray-200 transition-colors bg-white darken"><img class="w-full max-h-full" src={mod.LogoPath} /></button>
            {/each}
        </div>
    
        <div class="w-4/5  rounded p-3">
            <div class="bg-[red] w-full h-full emboss flex flex-col">
                <div class="bg-[wheat] flex-[1.414] max-h-[35%] rounded-[10px] m-3 mt-4 box-border flex justify-center">
                    <img src={currentMod.LogoPath} class="object-scale-down" alt="">
                </div>
                <div class="divider"></div>
                <div class="content flex-[2] bg-white m-4 flex flex-col relative">
                    <h1 class="text-center text-3xl font-bold text-green-500">{currentMod.Name}</h1>
                    <p class="downloads flex flex-col px-2">
                        {currentMod.Description == undefined ? "<MISSING>" : currentMod.Description}
                    </p>
                    <button
                     on:click={() => {
            if (document.startViewTransition) {
                document.startViewTransition(() => {
                                dialog.showModal()
                }) 
            }else {
                dialog.showModal()
            }

                        }}
                     class="absolute bottom-3 right-0 ml-auto mr-auto left-0 bg-purple-600 w-fit px-7 text-white font-bold text-xl rounded-xl hover:bg-purple-500 active:scale-90 transition-all hover:shadow-2xl shadow-black  py-2">Download</button>
                </div>
            </div>
        </div>
    </div>

    <a class="absolute bottom-5 left-5 bg-[url(https://moddersassociation.github.io/Almanac_IndexButton.png)] aspect-[164/26] h-[2vw] bg-cover pl-10 text-gray-800 hover:bg-[url(https://moddersassociation.github.io/Almanac_IndexButtonHighlight.png)]" href="/">Back</a>
</div>


<style>
    body {
        padding-inline: 10px;
    }
    .emboss {
        background-color: #bf8625;
        color: #000;
        border-radius: 10px;
        box-shadow: 0px 2px 4px 0px rgba(251,251,251,0.4) inset,
    0px 7px 13px -3px rgba(0,0,0,0.3),
    0px -3px 0px 0px rgba(0,0,0,0.2) inset;
    }
    .splide__slide {
        display: flex;
        justify-content: center;
        align-items: center;
    }
    
    </style>
