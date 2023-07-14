<script>
    import "papercss/dist/paper.min.css";
    import { Button, Form, Input, Select } from "spaper";

    let typeval = "default";
</script>

<section>
    <h1>F1 Notif bot settings</h1>
    <Form
        on:submit={(e) => {
            e.preventDefault();
            console.log("test");
        }}
    >
        <Input type="text" label="Event Name" />
        <Select label="Weekend Type" bind:value={typeval}>
            <option value="default">Normal Race Weekend</option>
            <option value="sprint">Sprint Race Weekend</option>
        </Select>
        <Input type="date" label="Weekend Start (the first friday)" />

        <Button type="primary">Submit?</Button>
    </Form>
</section>

<style>
    section {
        display: flex;
        background: darkgrey;
        flex-direction: column;
        min-height: 100vh;
        box-sizing: border-box;
        padding: 2rem;
    }

    h1 {
        line-height: 1.2;
        padding: 0;
        margin: 0;
    }
</style>
