<script>
    export let showModal = false;
    export let isPromo = false;
</script>

{#if showModal}
    <!-- class:promo={isPromo} will add a class "promo" if isPromo is evaluated to true -->
    <!-- on:click here is used to do event forwarding, the method we want to trigger is defined in
    an another file (App.svelte). So we will attach the method on the modal component
    in the parent file -->
    <div class="backdrop" class:promo={isPromo} on:click|self>
        <div class="modal">
            <slot name="title"></slot>
            <slot></slot>
        </div>
    </div>
{/if}

<style>
.backdrop {
    width: 100%;
    height: 100%;
    position: fixed;
    background: rgba(0, 0, 0, 0.8);
}

.modal {
    padding: 10px;
    border-radius: 10px;
    max-width: 400px;
    margin: 10% auto;
    text-align: center;
    background: white;
}

.promo .modal {
    background: crimson;
    color: white;
}
</style>