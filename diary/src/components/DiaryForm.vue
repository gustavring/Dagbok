<script setup>
    import { ref } from "vue";

    const emit = defineEmits(["add-post"]);

    const title = ref("");
    const date = ref("");
    const text = ref("");

    /* körs när formuläret skickas */
    function submitPost() {
        /* alla fält måste fyllas i */
        if (!title.value || !date.value || !text.value) {
        alert("Fyll i alla fält");
        return; 
        }

        emit("add-post", {
            title: title.value,
            date: date.value,
            text: text.value
        });

        /* tömmer fälten */
        title.value = "";
        date.value = "";
        text.value = "";
    }

</script>

<template>
    <form @submit.prevent="submitPost"> <!-- @submit.prevent för att köra funktionen utan att ladda om sidan -->
        <div class="title-wrapper">
            <label>Rubrik</label>
            <input v-model="title" placeholder="Ange rubrik" /> <!-- v-model kopplar input till title -->
        </div>

        <div class="date-wrapper">
            <label>Datum</label>
            <input v-model="date" type="date" placeholder="Ange datum" /> <!-- v-model kopplar input till date -->
        </div>

        <div class="text-wrapper">
            <label>Text</label>
            <textarea v-model="text" placeholder="Skriv ditt inlägg..."></textarea> <!-- v-model kopplar textarea till text -->
        </div>

        <button type="submit">Spara</button>
    </form>
</template>

<style scoped>
    form {
        display: flex;
        flex-direction: column;
        gap: 10px;

        background: #e6e6e6;
        padding: 15px;
        border-radius: 8px;

        margin-bottom: 20px;
    }

    .title-wrapper, .date-wrapper, .text-wrapper {
        display: flex;
        flex-direction: column;
    }

    input, textarea {
        padding: 8px;
        border: 1px solid #ccc;
        border-radius: 5px;
        font-size: 14px;
        max-width: 450px;
    }

    input {
        margin-bottom: 10px;
    }

    textarea {
        min-height: 100px;
    }

    button {
        padding: 10px;
        background: #2f4b80;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;

        transition: 0.2s ease;
    }

    label {
        color: rgb(77, 77, 77);
    }

    button:hover {
        background: #395b9b;
    }

    button:active {
        background: #2a4270;
    }
</style>
