<script lang="ts">
  interface Filter {
    label: string
    filter: string
    min: number
    max: number
    value: number
    unit: string
  }

  export let defaultFilter: Filter

  let filter: Filter = JSON.parse(JSON.stringify(defaultFilter))

  $: style = `filter: ${filter.filter}(${filter.value}${filter.unit})`
  $: title = filter.filter === 'none' ? filter.label : `${filter.label} ${filter.value}${filter.unit}`
</script>

<div class="relative flex flex-col w-64 p-4 font-mono bg-white shadow-lg place-items-center">
  <img class="object-cover" {style} src="http://placekitten.com/300/300" alt="kitten" />
  <h2 class="grid h-10 text-xl place-items-center">{title}</h2>
  {#if filter.filter !== 'none'}
    <div class="absolute inset-x-0 grid w-full bottom-1 place-items-center">
      <input type="range" class="w-11/12" min={filter.min} max={filter.max} bind:value={filter.value} />
    </div>
  {/if}
</div>
