<script>
  import { onMount } from "svelte";
  import AdviceCount from "./AdviceCount.svelte";

  $: advice = "Fast women and slow horses will ruin your life";
  $: count = 0;

  const getAdvice = async () => {
    const res = await fetch("https://api.adviceslip.com/advice");
    const data = await res.json();
    advice = data.slip.advice;
    count++;
  };

  onMount(() => {
    getAdvice();
  });
</script>

<div
  class="min-h-screen py-8 bg-slate-950 text-orange-50 grid place-content-center"
>
  <div
    class="max-w-lg bg-slate-800 p-8 m-6 rounded-lg border border-orange-400 shadow-md shadow-slate-800"
  >
    <h1
      class="text-3xl md:text-4xl xl:text-5xl text-center font-bold italic mb-8 before:content-[open-quote] after:content-[close-quote] before:text-orange-400 after:text-orange-400"
    >
      {advice}
    </h1>
    <div class="flex justify-between items-center gap-8">
      <AdviceCount {count} />
      <button
        on:click={getAdvice}
        class="px-6 py-2 border-2 border-orange-600 hover:bg-orange-500 hover:border-orange-500 font-bold rounded-full transition-colors duration-300"
      >
        Get Advice &rarr;
      </button>
    </div>
  </div>
</div>
