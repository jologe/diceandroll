<script lang="ts">
    import Dice from "../components/dice/Dice.svelte";
    import Roll from "../components/roll/Roll.svelte";
    import Header from "../components/utils/Header.svelte";
    import Footer from "../components/utils/Footer.svelte";
</script>

<Header />
<div class="grid-container">
    <div style="flex: 50%;">
        <Dice />
    </div>
    <div style="flex: 50%;">
        <Roll />
    </div>
</div>
<Footer />
