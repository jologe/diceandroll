<script lang="ts">
    import { onMount } from 'svelte';

    export let inString: string;
    let outcome: string[] = [];

    onMount(() => {
        printStringWithIntrigue(inString);
    });
    

    const generateRandomLetter = () => {
        const alphabet =
            "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
        return alphabet[Math.floor(Math.random() * alphabet.length)];
    };

    const printStringWithIntrigue = (str: string) => {
        for (let index = 0; index < str.length; index++) {
            setTimeout(() => {
                const interval = setInterval(() => {
                    outcome[index] =
                        `<span style='color: grey; font-weight: bold;'>${generateRandomLetter()}</span>`;
                }, 100);
                setTimeout(() => {
                    clearInterval(interval);
                    outcome[index] = inString[index];
                }, 400);
            }, index * 300);
        }
    };
</script>

<p style="display:inline">{@html outcome.join('')}</p>
