<script lang="ts">
    export let onSearch = (query: string) => {};
</script>

<input
    class="p-2 rounded-lg border border-stone-500 outline-none ring-transparent focus:ring-stone-400 ring-2 transition-all duration-300"
    type="text"
    placeholder="Search..."
    oninput={(e: Event & { currentTarget: HTMLInputElement }) =>
        onSearch(e.currentTarget.value || "")}
/>
