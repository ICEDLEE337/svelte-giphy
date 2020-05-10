<svelte:options tag="arc-card" />

<div class="arc-card">
<img class="icon" src={icon} alt="icon" />

</div>

<style style type="text/scss">
$icon-radius: 64px;

.arc-card {
    border-radius: 4px;
    box-shadow: 6px 6px 6px 6px rgba(0, 0, 0, 0.2);
    padding: 12px;
    display: flex;
    align-content: center;
    align-items: center;
    justify-items: center;
    background-color: yellow;
    width: $icon-radius * 3;
    height: $icon-radius * 5;

    .icon {
        width: $icon-radius;
        border-radius: $icon-radius;
        display: inline-block;
        background-color: violet;
    }
}
</style>

<script>
export let icon;
</script>