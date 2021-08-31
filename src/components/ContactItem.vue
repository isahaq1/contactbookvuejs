<template>
    <tr>
       <td>
            {{contact.title}}
       </td>
        <td>
            {{contact.phone}}
       </td>
        <td>
            {{contact.company}}
       </td>
        <td>
            {{contact.address}}
       </td>
        <td>
            {{contact.created_at}}
       </td>
        <td>
            {{contact.updated_at}}
       </td>
        <td>
           <button class="btn btn-info"> <i class="glyphicon glyphicon-pencil" @click="$emit('edit-contact-item', contact.id)"></i></button>
            <button class="btn btn-danger"><i class="glyphicon glyphicon-trash" @click="$emit('del-contact-item', contact.id)"></i></button>
             </td>
        
    </tr>
</template>

<script>
    export default {
        name: "ContactItem",
        props: ["contact"]
    }
</script>

<style scoped>
    .glyphicon-pencil, .glyphicon-trash{
        font-size: 15px;
        padding: 4px;
    }
</style>