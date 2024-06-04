<script lang="ts">
  import data from "./moddb.json"
  interface Mod {
  Name: string
  Versions: string[]
  DownloadLinks: string[]
  Description: string
  LogoPath: string
  Release: string
  Rating: number
  Screenshots: string[]
}

let Mods = data.Mods as Mod[]

let FeaturedMods = data.Featured.map((val, index) => {
  return Mods.filter((v2, i) => {
    return v2.Name == val
  })[0]
})

const sortByDate = (a: Mod, b: Mod) => {
    return new Date(a.Release).getTime() - new Date(b.Release).getTime();
};

// Sorting the array based on the 'date' property using the custom function
Mods.sort(sortByDate).splice(0,3);

</script>

<main>
  <nav class="h-[66vh] overflow-hidden bg-gradient-to-b from-red-800 via-red-400 to-red-300">
    <img src="malogo.webp" alt="logo" class="aspect-[1/0.9] h-[9rem]">
    <div id="curvecontainer" class="w-full flex justify-center mt-[5rem]">
      <div id="curve" class="aspect-square overflow-hidden bg-[url(stars.webp)] rounded-[50%] w-[120%] scale-125 z-3 grid justify-center">
        <img src="modpage.webp" alt="motm" class="relative object-cover"/>
      </div>
    </div>
  </nav>
  <main class="flex flex-col">
    <section class="flex h-16  text-white font-bold text-xl">
      <a class="new-mods-btn pointer flex-1 focus:text-2xl flex justify-center items-center gap-4">
        <img src="download.webp" class="w-10" alt="">
        New Mods
      </a>
      <a class="featured-mods-btn pointer flex-1 focus:text-2xl flex justify-center items-center gap-4">
        <img src="dl2.webp" class="w-10" alt="">
        Featured Mods
      </a>
    </section>
    <section class="mods flex">
      <div class="newmods flex flex-1 h-24 bg-[#EA580c] justify-evenly">
        {#if Array.isArray(Mods)}
          {#each Mods as mod}
            <a class="flex-1 border-l border-r border-orange-500 flex justify-center items-center">
              <img src={mod.LogoPath} alt={mod.Name} class="max-h-full">
            </a>
          {/each}
        {/if}
      </div>
      <div class="featuredmods flex flex-1 bg-[--newModsGradientColor2f]">
        {#if Array.isArray(FeaturedMods)}
          {#each FeaturedMods as mod}
            <a class="flex-1 border-l border-r border-orange-500 flex justify-center items-center">
              <img src={mod.LogoPath} alt={mod.Name} class="max-h-full">
            </a>
          {/each}
        {/if}
      </div>
    </section>
  </main>  
</main> 


<style>
    
.new-mods-btn {
    --newModsGradientColor1: rgb(253 224 71);
    --newModsGradientColor2: #EA580c;
    background: linear-gradient(var(--newModsGradientColor1), var(--newModsGradientColor2));
    transition: --newModsGradientColor1 .5s, --newModsGradientColor2 .5s, all .5s;
}

.new-mods-btn:hover {
    filter: brightness(80%);
}

.new-mods-btn:active {
    --newModsGradientColor2: rgb(253 224 71);
    --newModsGradientColor1: #EA580c;
}
.featured-mods-btn {
    --newModsGradientColor1f: #5bd4f1;
    --newModsGradientColor2f: #1668d2;
    background: linear-gradient(var(--newModsGradientColor1f), var(--newModsGradientColor2f));
    transition: --newModsGradientColor1f .5s, --newModsGradientColor2f .5s, all .5s;
}

.featured-mods-btn:hover {
    filter: brightness(80%);
}

.featured-mods-btn:active {
    --newModsGradientColor1f: #1668d2;
    --newModsGradientColor2f: #5bd4f1;
}

 section > .featured-mods-btn:focus {
    --newModsGradientColor2f: #5bd4f1;

 }
</style>