<script lang="ts">
  import Image from './components/Image.svelte'
  import Playground from './components/Playground.svelte'
  import Tailwind from './components/Tailwind.svelte'

  const config = {
    none: {
      min: 0,
      max: 0,
      value: 0,
      unit: '',
    },
    px: {
      min: 0,
      max: 20,
      value: 0,
      unit: 'px',
    },
    deg: {
      min: 0,
      max: 360,
      value: 0,
      unit: 'deg',
    },
    percent: {
      min: 0,
      max: 100,
      value: 0,
      unit: '%',
    },
    percent400: {
      min: 0,
      max: 400,
      value: 100,
      unit: '%',
    },
  }

  let filters = [
    { label: 'Original', filter: 'none', ...config.none },
    { label: 'Blur', filter: 'blur', ...config.px },
    { label: 'Opacity', filter: 'opacity', ...config.percent, value: 100 },
    { label: 'Sepia', filter: 'sepia', ...config.percent },
    { label: 'Hue Rotate', filter: 'hue-rotate', ...config.deg },
    { label: 'Brightness', filter: 'brightness', ...config.percent400 },
    { label: 'Contrast', filter: 'contrast', ...config.percent400 },
    { label: 'Saturate', filter: 'saturate', ...config.percent400 },
    { label: 'Grayscale', filter: 'grayscale', ...config.percent },
    { label: 'Invert', filter: 'invert', ...config.percent },
  ]
</script>

<Tailwind />

<div class="h-full bg-gray-100">
  <div class="max-w-6xl px-4 py-8 mx-auto text-gray-800">
    <h1 class="mb-8 text-xl font-bold text-center text-gray-700 sm:text-4xl">CSS Filter Preview</h1>
    <div class="grid grid-cols-1 gap-4 justify-items-center sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
      <div class="col-span-full">
        <Playground defaultFilters={filters.filter((f) => f.label !== 'Original')} />
      </div>
      {#each filters as defaultFilter, i (defaultFilter.label)}
        <Image {defaultFilter} />
      {/each}
    </div>
  </div>
</div>
