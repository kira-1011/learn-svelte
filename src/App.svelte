<script lang="ts">
    import TodoItem from "./lib/todo.svelte";
    import TodoSearch from "./lib/todo-search.svelte";
    import type { Todo } from "./types";
    let todos = $state<Todo[]>([
        {
            id: "1",
            text: "test",
            completed: false,
        },
        {
            id: "2",
            text: "dog",
            completed: false,
        },
        {
            id: "3",
            text: "cat",
            completed: false,
        },
        {
            id: "4",
            text: "bird",
            completed: false,
        },
        {
            id: "5",
            text: "fish",
            completed: false,
        },
        {
            id: "6",
            text: "apple",
            completed: true,
        },
        {
            id: "7",
            text: "banana",
            completed: false,
        },
    ]);

    let query = $state("");

    let filteredTodos = $derived(
        todos.filter((todo) =>
            todo.text.toLowerCase().includes(query.toLowerCase()),
        ),
    );

    const onSearch = (value: string) => {
        query = value;
    };

    const onComplete = (id: string, completed: boolean) => {
        todos.forEach((todo) => {
            if (todo.id === id) {
                todo.completed = completed;
            }
        });
    };
</script>

<main class="space-y-4">
    <h1 class="text-4xl font-bold">TODO APP</h1>

    <TodoSearch {onSearch} />

    {#each filteredTodos as todo}
        <TodoItem {todo} {onComplete} />
    {/each}
</main>
