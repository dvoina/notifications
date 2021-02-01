<script>
    export let title = "";
    export let id = "";

    import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

    async function deleteNotification() {
        console.log("sent delete for "+id);
        dispatch('message', {
            type: 'delete',
            notificationId:id
        });
    }

    async function muteNotification() {
        dispatch('message', {
            type: 'mute',
            notificationId:id
        });
    }
</script>

<style>

</style>

<li class="list-group-item">
    <span>{title}</span>
    <button class="btn btn-danger" on:click={deleteNotification}>Delete</button>
    <button class="btn btn-success"on:click={muteNotification}>Mute</button>
</li>