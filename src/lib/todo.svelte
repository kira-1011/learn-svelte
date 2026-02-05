<script lang="ts">
    import type { Todo } from "../types";
    export let todo: Todo;
    export let onComplete: (id: string, completed: boolean) => void;
</script>

<div
    class="p-4 border border-stone-700 rounded-md text-xl flex items-center gap-4"
>
    <input
        class="peer relative appearance-none shrink-0 w-4 h-4 border border-blue-200 rounded-sm mt-1 bg-white
               focus:outline-none focus:ring-offset-0 focus:ring-1 focus:ring-blue-100
               checked:bg-blue-500 checked:border-0
               disabled:border-steel-400 disabled:bg-steel-400 duration-300
             "
        type="checkbox"
        checked={todo.completed}
        onchange={(e: Event & { currentTarget: HTMLInputElement }) =>
            onComplete(todo.id, e.currentTarget.checked)}
    />
    <p class={todo.completed ? "line-through" : ""}>{todo.text}</p>
</div>
