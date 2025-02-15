<script>
  import "$lib/main.css";
  import { Button, Switch, Text, Card, ListItem, List, Accordion, Loading, ProgressBar, ToolTip, Numeric, Char, RadioElement, Modal, ComboBox, ComboBoxElement } from "$lib/index.js";
  
  let showModal = false;
  let toggle = false;
  let progress = 50;
  let selection = "1";
</script>

<Modal bind:state={showModal} closeButton={false}>
  <h2 slot="title">Modal Title</h2>
  <span>This is a modal content.</span>
  <Button slot="footer" onClick={() => (showModal = false)} type="danger"
    >Close</Button
  >
</Modal>

<div class="flex-v main">
  <h1>Welcome to this demo of @gzlab/uui</h1>
  <div class="cards">
    {#each new Array(3) as _, i}
      <Card size="sm">
        <svelte:fragment slot="title">Here is a Card {i}</svelte:fragment>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Earum quasi illo
        temporibus ratione facere beatae quam nobis culpa similique repellat doloribus
        odio, asperiores tempora? Quo deleniti facilis enim rem magnam?
        <span slot="footer">Lorem, ipsum dolor sit amet </span>
      </Card>
    {/each}
    {#each new Array(3) as _}
      <Accordion>
        <span slot="title">Accordion Header</span>
        <span>This is the accordion content.</span>
      </Accordion>
    {/each}
  </div>

  <Card size="sm">
    <List>
      <ListItem>
        Item 1
        <span slot="at">at 12:00</span>
        <span slot="subtitle">Lorem ipsum dolor sit amet</span>
      </ListItem>
      <ListItem>Item 2</ListItem>
      <ListItem>Item 3</ListItem>
    </List>
  </Card>

  <Card>
    <div class="flex">
      <Button onClick={() => (showModal = true)} primary>Open Modal</Button>
      <Button>Submit</Button>
      <ComboBox>
        <div class="selected" slot="selected">
          Option {selection}
        </div>
        <div class="list" slot="list">
          <ComboBoxElement value="1" bind:selection>Option 1</ComboBoxElement>
          <ComboBoxElement value="2" bind:selection>Option 2</ComboBoxElement>
          <ComboBoxElement value="3" bind:selection>Option 3</ComboBoxElement>
        </div>
      </ComboBox>
      <Text placeholder="Enter text" size="md" />
      <Numeric />
      <Char />
      <Button>Submit</Button>
    </div>
  </Card>

  <RadioElement group="options" value="1" checked>Option 1</RadioElement>
  <RadioElement group="options" value="2">Option 2</RadioElement>

  <Switch bind:checked={toggle} />

  <ProgressBar value={progress} />
  <Loading />

  <ToolTip>This is a tooltip</ToolTip>
</div>

<style>
  .flex {
    display: flex;
    gap: 0.4rem;
    flex-wrap: wrap;
  }

  .flex-v {
    display: flex;
    gap: 0.4rem;
    flex-direction: column;
  }

  .main {
    padding: 1rem;
    margin: auto;
    max-width: 1200px;
  }

  .cards {
    display: flex;
    flex-wrap: wrap;
    gap: 0.3rem;
    justify-content: center;
    align-items: start;
  }

  h1,
  h2 {
    text-align: center;
  }
</style>
