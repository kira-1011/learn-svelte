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

<h1 style="color: rgb({textColor})">Hello</h1>

<button onclick={() => changeColor()}>Change Color</button>
