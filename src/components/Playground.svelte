<script lang="ts">
  interface Filter {
    label: string
    filter: string
    min: number
    max: number
    value: number
    unit: string
  }

  export let defaultFilters: Filter[]

  let filters: Filter[] = JSON.parse(JSON.stringify(defaultFilters))

  function resetDefaults(): void {
    filters = JSON.parse(JSON.stringify(defaultFilters))
  }

  $: style = filters.map((f) => `${f.filter}(${f.value}${f.unit})`).join(' ')
</script>

<div class="grid w-full grid-cols-1 gap-4 p-8 mb-6 bg-white shadow-lg sm:grid-cols-2 justify-items-center">
  <img class="object-cover" style={`filter: ${style}`} src="http://placekitten.com/300/300" alt="kitten" />
  <div class="flex flex-col justify-evenly">
    {#each filters as filter, i (filter.label)}
      <div class="grid justify-between w-full grid-cols-3 gap-2">
        <div class="justify-self-end">{filter.label}</div>
        <input class="" type="range" min={filter.min} max={filter.max} bind:value={filter.value} step="5" />
        <span class="">{filter.value}</span>
      </div>
    {/each}
    <button class="mt-4" on:click={resetDefaults}>Reset Defaults</button>
  </div>
</div>
