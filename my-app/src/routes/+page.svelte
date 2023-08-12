<script>
    import * as BABYLON from 'babylonjs'
    import { onMount } from 'svelte'

    let num = 1;
    /**@type BABYLON.Engine*/ let engine;
    /**@type HTMLCanvasElement*/ let canvas;
    onMount(() => {
            engine = new BABYLON.Engine(canvas, true)
            const scene = new BABYLON.Scene(engine)
            const camera = new BABYLON.ArcRotateCamera("camera", -Math.PI / 2, Math.PI / 2.5, 3, new BABYLON.Vector3(0, 0, 0), scene)
            camera.attachControl(canvas, true)

            const light = new BABYLON.HemisphericLight("light", new BABYLON.Vector3(0, 1, 0), scene)

            const box = BABYLON.MeshBuilder.CreateBox("box", {}, scene)

            engine.runRenderLoop(() => scene.render())

        return () => engine.stopRenderLoop()
    })
</script>

<svelte:window on:resize={() => engine.resize()} />
<canvas bind:this={canvas}/>

<style>
    canvas {
        width: 100%;
        height: 100%;
    }

</style>
