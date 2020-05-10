<svelte:options tag='arc-cs'/>
<h1>CarSelector</h1>

<arc-hp></arc-hp>

<script>
import {onMount, beforeUpdate} from 'svelte';
import HierarchyPicker from '../components/HierarchyPicker.svelte';
let picker;
beforeUpdate(() => {
    picker = document.querySelector('arc-hp');
    // picker.provider = () => {
    //     return ['one', 'two', 'three'];
    // };

});

$: console.warn(picker);
</script>
