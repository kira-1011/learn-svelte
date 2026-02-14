<script lang="ts">
    import Cursor from "./cursor.svelte";
    import { onMount } from "svelte";

    let content =
        "lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat .";

    let attempts = $state<string[]>([]);
    let cursorPosition = $derived(attempts.length);

    const characters = content.split("");

    const clearAttempts = () => {
        attempts = [];
    };

    // Timer state
    let startTime = $state<number>(60);
    let timerInterval: ReturnType<typeof setInterval> | null = null;

    const startTimer = () => {
        timerInterval = setInterval(() => {
            startTime -= 1;
            if (startTime <= 0) {
                clearInterval(timerInterval!);
                clearAttempts();
            }
        }, 1000);
    };

    const formatTime = (seconds: number): string => {
        const mins = Math.floor(seconds / 60);
        const secs = seconds % 60;
        return `${mins}:${secs.toString().padStart(2, "0")}`;
    };

    const getCharClass = (index: number): string => {
        if (index >= cursorPosition) return "";
        if (attempts[index] === content[index]) return "text-green-400";
        return "text-red-400 bg-red-400/20";
    };

    const onKeyDown = (e: KeyboardEvent) => {
        if (e.key === "Backspace") {
            e.preventDefault();
            if (attempts.length > 0) {
                attempts.pop();
            }
        } else if (e.key.length === 1 && cursorPosition < content.length) {
            e.preventDefault();
            if (!timerInterval) {
                startTimer();
            }
            attempts.push(e.key);
        }
    };

    let containerEl: HTMLDivElement;

    onMount(() => {
        containerEl.focus();
        return () => {
            if (timerInterval) clearInterval(timerInterval);
        };
    });
</script>

<div class="text-2xl font-mono text-yellow-400 mb-4">
    {formatTime(startTime)}
</div>

<!-- svelte-ignore a11y_no_noninteractive_tabindex -->
<div
    class="text-[0px] font-mono outline-none whitespace-pre-wrap [&>span]:text-4xl [&>span]:leading-normal [&>span]:tracking-wider"
    tabindex="0"
    bind:this={containerEl}
    onkeydown={onKeyDown}
    role="textbox"
>
    {#each characters as char, i}
        {#if i === cursorPosition}<Cursor />{/if}
        <span class={getCharClass(i)}>{char}</span>
    {/each}
</div>
