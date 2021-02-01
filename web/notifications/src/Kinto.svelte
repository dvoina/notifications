<script>
    import Notification from './Notification.svelte';    

    export const backend = `${location.href}/v1/`;
    export const username = "admin";
    export const password = "secret";
    export const authorization = "Basic "+ btoa(`${username}:${password}`);

    export const kinto = new Kinto({
        remote: backend, 
        headers: {
            Authorization: authorization
        }
    });

    export const notifications = kinto.collection("notification");
    setInterval(listNotifications, 1000);


    var _notifications = [];

    $: listNotifications();


    async function listNotifications() {
        await notifications.sync({
            headers: {
                Authorization: authorization
            }
        });
        _notifications = (await notifications.list()).data;
    }

    async function createNotification() {
        console.log("Create new notification");

        // Create and store a new post in the browser local database
        await notifications.create({title: document.getElementById("title").value});
        
        // Publish all local data to the server, import remote changes
        listNotifications();
    }
    async function handleMessage(event) {
        console.log(event);
        if(event.detail.type=='delete') {
            await deleteNotification(event.detail.notificationId);
        }
        await listNotifications();
    }
    async function deleteNotification(id) {
        await notifications.delete(id);
    }

</script>

<div class="container">
    <h1>Notifications</h1>
    <div class="row">
    <div class="col-lg-6">
    <input id="title" class="form-control" type="text" name="title" placeholder="Thing">
    </div>
    <div class="col-lg-2">
    <button class="btn btn-primary" on:click={createNotification}>Create</button>
    </div>
    </div>
    <hr>
    <ul id="tasks" class="list-group">
    {#each _notifications as n}
        <Notification title="{n.title}" id="{n.id}" on:message={handleMessage}></Notification>
	{/each}
    </ul>
</div>

<style>

</style>