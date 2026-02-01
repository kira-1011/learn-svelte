<script>
    let textColor = $state("255,0,0");

    const changeColor = () => {
        let rgb = [
            Math.floor(Math.random() * 256),
            Math.floor(Math.random() * 256),
            Math.floor(Math.random() * 256),
        ];
        textColor = rgb.join(",");
    };
    $inspect(textColor);
</script>

<h1 class="bg-red-600">Hello</h1>

<button onclick={() => changeColor()}>Change Color</button>
